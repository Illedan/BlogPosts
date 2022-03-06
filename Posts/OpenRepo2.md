{"Tags":["Windows", "Mac", "Linux", "Tools"], "Id": "openrepoaddon", "Title": "Openrepo addons", "Description": "Utility tool for managing repositories", "Created": "2022-03-06", "Category": "Tools", "IsDraft": false}

# Openrepo

![Original post](https://www.kvanli.com/openrepo)

There are now additional configurations usable in the tool.

## Settings

Setup configuration for open repo. For now the only possible action is to ignore folders when finding files of certain types. An example is to ignore `node_modules` as it is a very big folder.

```
Settings:
    ignore bin
    ignore node_modules
```

## Clipboard

Copies the last phrase of the text to your clipboard.
```
Clipboard:
    DIS_ID 12345
```