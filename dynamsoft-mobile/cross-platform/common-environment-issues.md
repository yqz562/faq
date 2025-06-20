---
layout: default-layout
title: Common Environment Issues - Dynamsoft Barcode Reader for MAUI
description: This page introduce how to solve common environment issues when using Dynamsoft Barcode Reader MAUI SDK.
keywords: FAQ, maui, common environment issues
needAutoGenerateSidebar: true
needGenerateH3Content: true
noTitleIndex: true
---

# Common Environment Issues

## Failed to install

You might get "Could not find a part of the path 'C:\Users\admin\.nuget\packages\dynamsoft.imageprocessing.ios\2.2.300\lib\net7.0-ios16.1\Dynamsoft.ImageProcessing.iOS.resources\DynamsoftImageProcessing.xcframework\ios-arm64\dSYMs\DynamsoftImageProcessing.framework.dSYM\Contents\Resources\DWARF\DynamsoftImageProcessing'" error when installing the package on a **Windows** PC. That's because the Windows system have a limitation of 260 characters in the path. There are 2 ways to solve this:

### Exclude the iOS platform from the project

The long path belongs to the iOS xcframework of the package. If you only want to run Android on Windows, you can use this solution.

Remove iOS platform from you project via the project file.

```xml
<PropertyGroup>
    <!-- Remove iOS and desktop platforms from your TargetFrameworks. -->
    <!-- <TargetFrameworks>net8.0-android;net8.0-ios;net8.0-maccatalyst</TargetFrameworks> -->
    <TargetFrameworks>net8.0-android</TargetFrameworks>

    <SupportedOSPlatformVersion Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)')) == 'android'">21.0</SupportedOSPlatformVersion>
    <!-- Remove the iOS platforms from the SupportedOSPlatformVersion. -->
    <!-- <SupportedOSPlatformVersion Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)')) == 'ios'">11.0</SupportedOSPlatformVersion> -->
</PropertyGroup>
```

### Add the library via project file instead of **Nuget Package Manager**

Adding the library via project file can ignore the 260 character limitation but you need some additional steps to complete the installation.

```xml
<Project Sdk="Microsoft.NET.Sdk">
    ...
    <ItemGroup>
        ...
        <PackageReference Include="Dynamsoft.BarcodeReaderBundle.Maui" Version="10.2.1101" />
    </ItemGroup>
</Project>
```

Open the **Package Manager Console** and run the following commands:

```bash
dotnet build
```

## error NU1202: Package Dynamsoft.BarcodeReaderBundle.Maui 10.2.1101 is not compatible with net8.0-windows10.0.19041

You may find similar issues like:

- "not compatible with net8.0-windows10.0.19041"
- "not compatible with net8.0-maccatalyst17.2"

Currently, `Dynamsoft.BarcodeReaderBundle.Maui` library doesn't support desktop environment. You have to remove them from your project.

```xml
<PropertyGroup>
    <!-- Remove ";net8.0-maccatalyst" from your TargetFrameworks. -->
    <!-- <TargetFrameworks>net8.0-android;net8.0-ios;net8.0-maccatalyst</TargetFrameworks> -->
    <TargetFrameworks>net8.0-android;net8.0-ios</TargetFrameworks>
    <!-- Remove "net8.0-windows10.0.19041.0" from your TargetFrameworks. -->
    <!-- <TargetFrameworks Condition="$([MSBuild]::IsOSPlatform('windows'))">$(TargetFrameworks);net8.0-windows10.0.19041.0</TargetFrameworks> -->

    <SupportedOSPlatformVersion Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)')) == 'ios'">11.0</SupportedOSPlatformVersion>
    <SupportedOSPlatformVersion Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)')) == 'android'">21.0</SupportedOSPlatformVersion>
    <!-- Remove the unsupported platforms from the SupportedOSPlatformVersion. -->
    <!-- <SupportedOSPlatformVersion Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)')) == 'maccatalyst'">13.1</SupportedOSPlatformVersion> -->
    <!-- <SupportedOSPlatformVersion Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)')) == 'windows'">10.0.17763.0</SupportedOSPlatformVersion>
    <TargetPlatformMinVersion Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)')) == 'windows'">10.0.17763.0</TargetPlatformMinVersion>
    <SupportedOSPlatformVersion Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)')) == 'tizen'">6.5</SupportedOSPlatformVersion> -->
</PropertyGroup>
```
