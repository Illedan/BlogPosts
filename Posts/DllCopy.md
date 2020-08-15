{"Tags":["Windows","Tools"], "Title": "Dll Copy", "Description": "Utility tool for Windows development", "Created": "2020-02-23", "Category": "Tools"}

# DllCopy

[Github source code](https://github.com/Illedan/DllCopy)

DllCopy is an utility tool to copy files from a location to another. It is called DllCopy because the initial need was for C# development.

![Layout](https://github.com/Illedan/DllCopy/blob/master/Capture.PNG "DllCopy")


## Usage

- Add items to the left by using Add folder and adding files
    - Adding files is equal to adding the Path/location on disk for that file. Not the file itself. This enables the user to update files without touching dllcopy.
- Add targets by finding applications with New Targets
- Select your wanted target and use commands. :rocket:
- Icons can be found: http://modernuiicons.com/ or any other place with SVG paths availiable.

## Copy

Copying will result in files added to the target destination with regards to their position in the folder structure you created.

For example:

- MyProject
    - Folder1
        - Folder2
            - FileInFolder2
        - FileInFolder1
    - FileOutsideFolder

Copied to a target:

Initial layout:
- MyTarget.exe


After copy:
- MyTarget.exe
- FileOutsideFolder
- Folder1
    - Folder2
        - FileInFolder2
    - FileInFolder1


