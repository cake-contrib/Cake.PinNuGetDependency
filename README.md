## Cake.PinNuGetDependency 

Are you using the new `dotnet pack` tooling to create your NuGet packages and are frustrated that there is no way to specify that child packages of our main project should be *locked* to the version that's being built? Not having version pinning creates user frustration when using bait & switch style libaries and is it's own special type of hell for maintainers to support. This Cake addin unzips the specified NuGet package and searches of the supplied dependency and locks the version.


## Installation

Add the following reference to your cake build script:

```csharp
#addin "Cake.PinNuGetDependency"
```

## Usage

```csharp
var filePath = new FilePath(@"./artifacts/reactiveui-xamforms-8.0.0.nupkg");
PinNuGetDependency(filePath, "reactiveui");
```

Which does the following

* Opens `reactiveui-xamforms-8.0.0.nupkg` in memory
* Extracts the nuspec definition and modifyes the dependency version of `reactiveui` to be `$"[{$version}]"`
* Saves contents of memory to `reactiveui-xamforms-8.0.0.nupkg`