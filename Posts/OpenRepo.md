{"Tags":["Windows", "Mac", "Linux", "Tools"], "Id": "openrepo", "Title": "Openrepo", "Description": "Utility tool for managing repositories", "Created": "2019-09-26", "Category": "Tools", "IsDraft": false}

# Openrepo

Utility tool for managing repositories which utilizes console to give better screen navigation.
Keep a console open with this tool running and use it as your main source of navigation.

Nuget package: https://www.nuget.org/packages/Illedan.OpenRepo/0.0.25
Code: https://github.com/Illedan/OpenRepo

## Prerequisits

- `dotnet` installed on the machine.

## Installation

`dotnet tool install --global Illedan.OpenRepo`

## Update

`dotnet tool install --update Illedan.OpenRepo`

## Usage

Once the tool is installed you can use the console command `openrepo`. This will start the tool and show the config in your default `.txt` editor if it is your first startup.

### Searching

Once you have your configuration set up, you can use the Arrow keys to navigate up and down or start typing to filter the list. Use space to filer on multiple words, as example:
```
Filter: Project Xamarin
Hits: Project.Test.Xamarin, Xamarin.Project, XamarinProject, Xamarin Project Other, etc.
```

Use `ENTER` to select an option and `TAB` to refresh with new config values if you updated elsewhere.
Once an option is selected a set of sub-options are shown (unless there is only 1 which is activated instantly)

### Configuration

Use `OpenRepo - Edit config` option to open the configuration file. This command is searchable like every other item you add to the list.

The configuration is a txt file located in appdata on Windows and application data on Mac. The initial config created contains examples starting with `#` making that line a comment. Example:
```
# Welcome to OpenRepo
# Created by https://github.com/Illedan 
# Add this path. Where C:/Repos/ is replaced with your repo location
Local:
    C:/Repos/ pt:sln pt:bat

Personal:
    nuget https://www.nuget.org
```

Lines starting far left is considered a Provider and every line below it with indentation is configuration used by that Provider (see provider information below).

If your path contain spaces you have to wrap it in '"'. Ex:
```
Local:
    "C:/Location with space/Repos" pt:sln ptt:bat 

Personal:
    "nuget openrepo package example" "https://www.nuget.org/packages/Illedan.OpenRepo/"
```

## Providers

### Local

Example:
```
Local:
    C:/repos prefix:repos/ pt:sln ptt:md
    /Users/Illedan/Projects/ prefix:projects/
```

Finds all folders inside a folder.

Possible Parameters:
- `prefix:customname` Applies `customname` in front of all folder from this source. Needed if you have many equal names. (Recommended to add a divider like / at the end)
- `pt:programtype` Adds Actions to start extensions of programtype. Example is `pt:sln` which finds all solutions inside the repo. Logs if there is none, starts the first if one and gives a list to select if there are multiple.
- `ptt:programtype` Adds Actions to start extensions of programtype. Example is `ptt:md` which finds all solutions inside the repo on the root level. Logs if there is none, starts the first if one and gives a list to select if there are multiple.

Actions:
- `Open` Opens the folder in explorer/finder
- `Web` Opens a browser to the remote location of the repository. Only shows if this is a git repository.

### Personal

Here you can add a key + a value to link to. As the example here:
```
Personal:
    nuget https://www.nuget.org
    "cool user" https://www.github.com/Illedan
```
`nuget` would send the user to nuget.org and `cool user` to Illedan's github profile.
This could also be folders in your file system, scripts, programs, files, online resources, etc.

## Running on Windows with AutoHotkey
One approach to working with openrepo on a windows machine is to use an AutoHotkey script to fire it and if it is already running, just bring it in to view.

First, you will need to install AutoHotkey https://www.autohotkey.com/.

Go to your desktop and right click, new, AutoHotkey Script.

```
F1::
IfWinExist C:\Users\<USER>\.dotnet\tools\OpenRepo.exe
{
  WinActivate, C:\Users\<USER>\.dotnet\tools\OpenRepo.exe
}
else
{
    run, OpenRepo
    WinActivate, C:\Users\<USER>I\.dotnet\tools\OpenRepo.exe
}
```
This script will trigger when the ```F1``` key is pressed

Finally run the AutoHotkey script by double clicking it. 

Openrepo should now come in to view when pressing F1

### Snake

```
Snake:
    100
```
Fun addon to play snake within the tool itself. The time indicates time between each move. Higher speed equals more point each food. Use arrow keys to navigate, `ENTER` to restart and `ESC` to quit. Good luck & Have Fun :) 

## Issues

Selecting `OpenRepo - Create issue` navigates you to the github page of this project with the last exception set as body for an Issue.

Any other issue or question is also welcome :) 

