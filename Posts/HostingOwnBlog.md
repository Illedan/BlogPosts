{"Tags":["Hosting", "Nginx", "Blog"], "Id":"blogsetup", "Title": "Hosting the blog", "Description": "Post mortem of hosting this blog with Nginx on Digital Ocean", "Created": "2020-08-21", "Category": "Blog", "IsDraft": true }

# Hosting the blog

tl&dr: Blog is hosted on Digital Ocean by using Nginx as a Reversed Proxy. Backend is a Node server running in PM2 while consuming a SQLite database. The Web page is created in Vue and is simply static pages pointed to by Nginx. And "Security" through HTTPS by Let's Encrypt, using certificates created by Certbot.

The intention of this post is to describe how I created this blog. It will, hopefully, serve as a guide and contain explainations on how to do it yourself. Feel free to ask me on Twitter if you have questions.

I would love corrections or guides if I did something terribly wrong or insufficient, as it is the first time I host the whole thing myself. (I know there are platforms for blogging, but the intention of this blog is for my own learning.)

## Hosting

First things first, needed a place to run everything. I have some old computers, but setting it up in the cloud feels safer and it is easier to follow guides or recreated everything if I fail.. I got recommended Digital Ocean some time back and found it cheap enough to not bother checking further. For 5 $ /month I got these specs:
- Ubuntu 18.04.3 (LTS) x64
- 1 vCPUs
- 1 GB RAM
- 25 GB Disk

Should be decent enough to keep the blog alive. I might consider uppgrading it to 2 CPUs if I get some readers or start doing something slightly more serious. (though I would need metrics to verify it being slow)

## Domain

Bought a domain of (namecheap.com)[https://www.namecheap.com] and followed the instructions in (this post)[https://www.digitalocean.com/community/tutorials/how-to-point-to-digitalocean-nameservers-from-common-domain-registrars].

Why namecheap? No idea. I guess any provider would work.

## Nginx

Guide to (setup Nginx)[https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-18-04]

()
Create file for my domain in `/etc/nginc/sites-availiable/kvanli.com.conf`

### HTTPS

Luckily for developer these days, there is something called Let's Encrypt which provides Certbot. Certbot automatically renews the certificate obtained for the Domain once configured. 

I used (this guide)[https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-18-04] to Certbot


### Final config

```C#
server {
     server_name kvanli.com www.kvanli.com;
     index index.html index.htm;

     location /api{
      proxy_pass http://localhost:5555
      proxy_http_version 1.1;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection 'upgrade';
      proxy_set_header Host $host;
      proxy_cache_bypass $http_upgrade;
     }

     location / {
         alias /vuelocation/dist/;
         try_files $uri $uri/ =404;
     }

    listen [::]:443 ssl ipv6only=on; # managed by Certbot
    listen 443 ssl; # managed by Certbot
    ssl_certificate ...pem; # managed by Certbot
    ssl_certificate_key ...pem; # managed by Certbot
    include ...conf; # managed by Certbot
    ssl_dhparam ...pem; # managed by Certbot
}

server {
    if ($host = www.kvanli.com) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


    if ($host = kvanli.com) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


     listen 80;
     listen [::]:80;
     server_name kvanli.com www.kvanli.com;
    return https://kvanli.com/web; # managed by Certbot
}
```


## Posts

```json
{"Tags":["Hosting", "Nginx", "Blog"], "Id":"blogsetup", "Title": "Hosting the blog", "Description": "Post mortem of hosting this blog with Nginx on Digital Ocean", "Created": "2020-08-21", "Category": "Blog", "IsDraft": true }
```
I have to write a json on the first line of every post, which could be seen in the example above (as taken from this post).
- Tags: Tags used to group posts
- Id: Used as an unique identifier when I Replace into the database
- Title and Description: About the post
- Created: Time of creation - Might consider adding Time of writing, as the intention of Created is when the focus of the post was created.
- Category: To divinde into segments if users would continue inside the same Category. Though I should rather use Machine Learning to group posts on user groups.
- IsDraft: Used to remove the post from lists unless opted in. For me to test it in production before readers get it.

