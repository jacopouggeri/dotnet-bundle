# dotnet-bundle

Command-line interface tools for bundling .NET Core projects into MacOS applications (.app)

### Installation

Install MSBuild task via NuGet package: `Dotnet.Bundle`

[![NuGet](https://img.shields.io/nuget/v/Dotnet.Bundle.svg)](https://www.nuget.org/packages/Dotnet.Bundle/)

```
<PackageReference Include="Dotnet.Bundle" Version="*" />
```

### Using the tool

```
dotnet msbuild -t:BundleApp -p:RuntimeIdentifier=osx-x64 [-p: ...]
```

### Properties

Define properties to override default bundle values. Check [TestBundle.csproj](TestBundle/TestBundle.csproj) for a working example.

```
<PropertyGroup>
    <CFBundleName>AppName</CFBundleName> <!-- Also defines .app file name -->
    <CFBundleDisplayName>App Name</CFBundleDisplayName>
    <CFBundleIdentifier>com.example.app</CFBundleIdentifier>
    <CFBundleShortVersionString>1.0.0</CFBundleShortVersionString>
    <CFBundleVersion>1.0.0</CFBundleVersion>
    <CFBundlePackageType>APPL</CFBundlePackageType>
    <CFBundleSignature>????</CFBundleSignature>
    <CFBundleExecutable>AppName</CFBundleExecutable>
    <CFBundleIconFile>AppName.icns</CFBundleIconFile> <!-- Will be copied from output directory -->
    <NSHighResolutionCapable>true</NSHighResolutionCapable>
</PropertyGroup>

<!-- Optional URLTypes -->
<ItemGroup>
    <CFBundleURLTypes Include="dummy"> <!-- The name of this file is irrelevant, it's a MSBuild requirement.-->
        <CFBundleURLName>TestApp URL</CFBundleURLName>
        <CFBundleURLSchemes>testappurl;testappurl://</CFBundleURLSchemes> <!-- Note the ";" separator-->
    </CFBundleURLTypes>
    <CFBundleURLTypes Include="dummy">
        <CFBundleURLName>TestApp URL2</CFBundleURLName>
        <CFBundleURLSchemes>test://</CFBundleURLSchemes>
    </CFBundleURLTypes>
</ItemGroup>
```

More info: https://developer.apple.com/library/archive/documentation/CoreFoundation/Conceptual/CFBundles/BundleTypes/BundleTypes.html
