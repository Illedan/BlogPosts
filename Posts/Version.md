{"Tags":["Linux", "DotNet"], "Id": "version", "Title": "Automatic version", "Description": "Getting automatic patch bump during github action", "Created": "2020-12-30", "Category": "Tools", "IsDraft": false}

# Automatic version

I find that most of my commits on private packages is related to patch updates, making updates of version files tedious. Tagging works, but I would end up making an abstraction on top of tags to force major, minor or patch without me having to think too much. I wanted to add automatic versioning and publishing of [OpenRepo](https://kvanli.com/stories/openrepo) whenever I pushed to master.

## Version file

I created a version.config file on the root of my project and added : '1.0' (my current version). To read this into an environment variable I used cat and some regex to remove unwanted chars:
```
    - name: Read VERSION file
      id: getversion
      run: echo "::set-output name=version::$(cat version.config | grep -oh "[0-9]\.[0-9]")"
```

The reason for this grep is an unwanted <FEFF> char appearing in front of my version for no particular reason, costing me more time than I care to admit as it was invisible in every editor, terminal, browser I tried. 
(╯°□°)╯︵ ┻━┻  

This environment variable is found by using `${{ steps.getversion.outputs.version }}`.

## Packing

Dotnet pack has a convenient argument of `-p:Version` which sets the version of the project. Making me able to use the version from my version file together with the Github run number. To the smart eye you could see that patch will never reset itself, but I don't see this as a problem on this project.

```
    - name: Pack
        run: dotnet pack src/OpenRepo/ -p:Version=${{ steps.getversion.outputs.version }}.${GITHUB_RUN_NUMBER}
```

## Publishing

I created a publish key on nuget.org and added it to the Secrets of my Repository. I did add it as an Environment secrets first, which obviously didn't work..

Using this while targetting the packed .nupkg caused the package to be pushed nicely to nuget.org 🎉

```
    - name: Publish Nuget
      run: dotnet nuget push src/OpenRepo/nupkg/*.nupkg --source https://api.nuget.org/v3/index.json --api-key ${{ secrets.NUGETORG }} --skip-duplicate
```

## Result

[Publish file](https://github.com/Illedan/OpenRepo/actions/runs/452913812/workflow)
[Nuget OpenRepo](https://www.nuget.org/packages/Illedan.OpenRepo/)