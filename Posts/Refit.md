{"Tags":["DotNet", "NuGet"], "Id": "refit", "Title": "Refit", "Description": "Rest library for .NET", "Created": "2022-02-03", "Category": "DotNet", "IsDraft": false}

# Refit
 
[Refit](https://github.com/reactiveui/refit) is a type-safe REST library for .NET found on NuGet created by ReactiveUI.
 
Instead of fiddling with various Rest clients, services or whatnot, all you need is to create an interface, which can be stored in a shared Project for various Applications
 
```
public interface IApi
{
    [Get("/api/{id}")]
    Task<Data> Get(string id);
}
```
and creating it with your httpclient: (or use the 'services.AddRefitClient<IApi>()' in asp.net)
```
var api = RestService.For<IApi>("https://myurl.com")
```
and using it
```
var data = await api.Get("id");
```

This would remove a lot of overhead and magic implementations of API usage, as you can create a sweet uniform way of handling your APIs.