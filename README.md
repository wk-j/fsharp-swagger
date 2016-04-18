Registry additions have been made in order to provide you the best web development experience.

See http://bloggemdano.blogspot.com/2013/11/adding-new-items-to-pure-f-aspnet.html for more information.


### Create project

```bash
yo fsharp
```

### Issue

```bash
╰─$ xbuild
XBuild Engine Version 14.0
Mono, Version 4.4.0.0
Copyright (C) 2005-2013 Various Mono authors

Build started 4/18/2016 11:42:44 PM.
__________________________________________________
Project "/Users/wk/Source/fsharp/fsharp-swagger/fsharp-swagger/fsharp-swagger.fsproj" (default target(s)):
        Target BeforeBuild:
: error : Error initializing task MSBuild.ExtensionPack.FileSystem.File: Not registered task MSBuild.ExtensionPack.FileSystem.File.
                Build FAILED.
                Errors:
                /Users/wk/Source/fsharp/fsharp-swagger/fsharp-swagger/fsharp-swagger.fsproj (default targets) ->
                (BeforeBuild target) ->
                        : error : Error initializing task MSBuild.ExtensionPack.FileSystem.File: Not registered task MSBuild.ExtensionPack.FileSystem.File.
                         0 Warning(s)
                         1 Error(s)
                Time Elapsed 00:00:00.1794100
```

### Fixed

Convert `..` to `$(MSBuildProjectDirectory)`

```xml
<UsingTask
    AssemblyFile="..\packages\MSBuild.Extension.Pack\tools\net40\MSBuild.ExtensionPack.dll"
    TaskName="MSBuild.ExtensionPack.FileSystem.File"
    Condition="Exists('..\packages\MSBuild.Extension.Pack\tools\net40\MSBuild.ExtensionPack.dll')" />
```

```xml
<UsingTask
    AssemblyFile="$(MSBuildProjectDirectory)\packages\MSBuild.Extension.Pack\tools\net40\MSBuild.ExtensionPack.dll"
    TaskName="MSBuild.ExtensionPack.FileSystem.File"
    Condition="Exists('$(MSBuildProjectDirectory)\packages\MSBuild.Extension.Pack\tools\net40\MSBuild.ExtensionPack.dll')" />
```

### Add dependencies

```
paket add nuget Microsoft.AspNet.WebApi.OwinSelfHost project fsharp-swagger.fsproj
```

### Compile and run

```
./run.sh
```

### Test

```
http://localhost:9000/api/value/get
```