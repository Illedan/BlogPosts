{"Tags":["Windows", "Mac", "Linux", "CodinGame", "Tools"], "Id": "csharpmerger", "Title": "C# file merger", "Description": "Utility program to merge C# files into one for CodinGame usage.", "Created": "2020-03-20", "Category": "Tools", "IsDraft": true}

# C# merger

This is a tool to merge multiple C# files into 1 file, while merging the `using` statements to avoid duplicates. The usecase for this tool is CodinGame where you can only submit 1 file. Personally I use it together with [CG-sync](https://www.codingame.com/forum/t/codingame-sync-beta/614) where I point CG-sync to the output file.

- clone https://github.com/Illedan/CG-sharpmerger
- cd /CG-sharpmerger/src/CSharpMerger
- dotnet run
- Write or paste the root of the files you want to be merged
    - Example: Use repo/src
        - repo/src
        - Test.csproj
        - Program.cs
            - /models
                - Data.cs
- Then write the target file. In the previous example: repo/Output.cs
    - It is accepted to add the file inside the repo itself, but that might confuse the project file. (unless you add a different filextension than .cs)
- Start coding! And watch the Updated notification in the console keep posting. 

It is only checking for updates every 0.5 sec and CG-sync might be a little slow too, but look for the part:
``` // LastEdited: 31/08/2020 0:32  ```
which will be added to your code below the using statements, as it is injected by the merger to provide proof of updates.