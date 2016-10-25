# Use dotnet tools extensibility to bootstrap tools like Paket

A dotnet tool is just a console app built for `netcoreapp1.0` but name should
be `dotnet-{name}`. The package name doesnt matter, it's important only the executable
name

Just add a `DotNetCliToolReference` in the projects (fsproj, csproj, doesnt matter).

```xml
  <ItemGroup>
    <DotNetCliToolReference Include="mytool">
      <Version>1.0.0-preview2-*</Version>
    </DotNetCliToolReference>
  </ItemGroup>
```
And Restore.
After that, is avaiabile as `dotnet mytool` from the same directory


## Paket boostrapper

Ideas is, use a msbuild project with all the tools for repo.
For example Paket but can be others (for docs, fake, etc)

In the example i use an existing tool `dotnet-mergenupkg`, but is not special

User flow

- dotnet restore3 tools.toolsproj
    restore just the project with tools. extension doesnt matter, but suffix must be `proj`
- dotnet mergenupkg
    run the tool

So ideally to bootstrap Paket

- dotnet restore3 tools.toolsproj
    restore just the project with tools. extension doesnt matter, but suffix must be `proj`
- dotnet paket
    run Paket

You can also run `dotnet paket` from targets file.
