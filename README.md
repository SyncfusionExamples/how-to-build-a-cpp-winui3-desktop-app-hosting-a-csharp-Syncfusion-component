# how-to-build-a-cpp-winui3-desktop-app-hosting-a-csharp-Syncfusion-component

## Overview

This sample demonstrates how to build a C++/WinUI 3 desktop application that hosts a Syncfusion C# runtime component (SfDataGrid). The C# component (SfDataGrid) is part of the WinUI 3 controls and is successfully consumed within a C++/WinRT application using the Windows App SDK. The component was referenced in the C++/WinRT app by following the official walkthrough: [Create a C# component with WinUI controls, and consume it from a C++/WinRT app that uses the Windows App SDK - Microsoft Learn](https://learn.microsoft.com/en-us/windows/apps/develop/platform/csharp-winrt/create-winrt-component-winui-cswinrt).

## Prerequisites

To build and run this sample, ensure you have the following installed on your Windows development machine:

- **Windows 10, version 1809 (build 17763)** or later, or **Windows 11**
- **Visual Studio 2022** (17.0 or later) with the following workloads:
  - Universal Windows Platform development
  - Desktop development with C++
  - .NET desktop development
- **Windows App SDK** (latest stable version)

## Project Structure

The repository contains two top-level folders, each with its own solution file:

```
how-to-build-a-cpp-winui3-desktop-app-hosting-a-csharp-Syncfusion-component/
├── CppApp/                        # C++/WinUI 3 host application
│   ├── CppApp.sln
│   └── CppApp/
│       ├── App.xaml / App.xaml.cpp / App.xaml.h
│       ├── MainWindow.xaml / MainWindow.xaml.cpp / MainWindow.xaml.h
│       ├── MainWindow.idl
│       ├── Package.appxmanifest
│       ├── app.manifest
│       ├── packages.config
│       ├── pch.cpp / pch.h
│       ├── CppApp.vcxproj / CppApp.vcxproj.filters
│       ├── Assets/
│       └── Generated Files/       # Auto-generated C++/WinRT projections
└── AuthoringWinUI/                # C# WinUI 3 component library
    ├── AuthoringWinUI.sln
    └── WinUIComponentCs/
        ├── NameReporter.xaml / NameReporter.xaml.cs
        ├── OrderInfo.cs           # Data model
        ├── ViewModel.cs           # DataGrid view model
        └── WinUIComponentCs.csproj
```

### Projects

1. **CppApp** (C++/WinRT desktop application, WinUI 3) — Located in `CppApp/`. This is the host application that consumes the C# WinUI 3 component. It is built using the C++/WinRT projection generated from the C# class library.
2. **WinUIComponentCs** (C# class library) — Located in `AuthoringWinUI/WinUIComponentCs/`. This project defines the WinUI 3 `UserControl` (`NameReporter`) that hosts the Syncfusion `SfDataGrid`, along with the data model (`OrderInfo`) and view model (`ViewModel`).

## How It Works

The C# project (`WinUIComponentCs`) defines a WinUI 3 `UserControl` named `NameReporter` that contains a Syncfusion `SfDataGrid` populated with sample order data (from `OrderInfo` and `ViewModel`). The C++/WinRT project (`CppApp`) adds a project reference to this C# component and includes the auto-generated C++/WinRT projection headers (found under `Generated Files/`).

During build, the C#/WinRT tooling generates a WinRT projection (`.winmd` and C++/WinRT headers) from the C# assembly, allowing the C++ host to consume the C# types as native WinRT types. The C# runtime is loaded automatically when the C++ app starts, and the WinUI 3 control is hosted within the native C++/WinUI 3 `MainWindow`.

## Build and Run

1. Clone this repository to your local machine.
2. Open the solution file (`CppApp.sln`) in **Visual Studio 2022**.
3. Set CppApp as the startup project—right-click on CppApp, and select Set as Startup Project. 
4. Set the configuration to **x86** (recommended).
5. Build the solution (`Ctrl+Shift+B`).
6. Set the C++/WinRT desktop project as the startup project and press `F5` to run.

> **Note:** The `CppApp.sln` already references the `WinUIComponentCs` C# project (under `../AuthoringWinUI/WinUIComponentCs/`), so the WinUI 3 C# component is built automatically as part of the solution. NuGet packages must be restored before the first build.

## Key Learnings

- How to author a WinUI 3 control in **C#** and expose it to a **C++/WinRT** consumer.
- How to integrate **Syncfusion WinUI controls** (SfDataGrid) into a native C++/WinUI 3 desktop application.
- How the **C#/WinRT projection** enables interop between managed (C#) and native (C++/WinRT) code.
- How to configure project references, NuGet packages, and runtime activation for mixed-language WinUI 3 apps.

## References

- [Create a C# component with WinUI controls, and consume it from a C++/WinRT app that uses the Windows App SDK](https://learn.microsoft.com/en-us/windows/apps/develop/platform/csharp-winrt/create-winrt-component-winui-cswinrt)
- [Windows App SDK documentation](https://learn.microsoft.com/en-us/windows/apps/windows-app-sdk/)
- [Syncfusion WinUI DataGrid (SfDataGrid)](https://help.syncfusion.com/winui/datagrid/getting-started)  