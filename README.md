# Xamarin Workbooks

| macOS               | Windows             |
| ------------------- | ------------------- |
| ![][macbuildstatus] | ![][winbuildstatus] |

Xamarin Workbooks provide a blend of documentation and code that is perfect
for experimentation, learning, and creating guides and teaching aids.

Create a rich C# workbook for .NET Core, Android, iOS, Mac, or WPF, and get
instant live results as you learn these APIs. Workbooks also have access to
the vast NuGet package ecosystem to make learning new APIs a breeze.

## Resources

### Download

* [Download Latest Public Release for Mac](https://dl.xamarin.com/interactive/XamarinInteractive.pkg)
* [Download Latest Public Release for Windows](https://dl.xamarin.com/interactive/XamarinInteractive.msi)

### Documentation

* [Workbooks Documentation](https://developer.xamarin.com/guides/cross-platform/workbooks/)
* [Live Inspection Documentation](https://developer.xamarin.com/guides/cross-platform/inspector/)
* [Sample Workbooks](https://github.com/xamarin/Workbooks)

### Provide Feedback

* [Discuss in Xamarin Forums](https://forums.xamarin.com/categories/inspector)
* [File Bugs](https://bugzilla.xamarin.com/enter_bug.cgi?product=Workbooks%20%26%20Inspector)

## Build & Run

### External Build Dependencies & Development Environment

We generally track the latest (usually stable, but sometimes preview) releases
of the Visual Studio / Xamarin release cycles. Below are complete sets of
dependencies for building Workbooks on macOS and Windows. The dependency lists
are generated by our VSTS build machines.

#### macOS Dependencies

| Component                       | Version      | Download                                                                                                                                                          |
| :------------------------------ | :----------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NuGet CLI                       | 4.3.0        | [nuget.exe](https://dist.nuget.org/win-x86-commandline/v4.3.0/nuget.exe)                                                                                          |
| Xcode                           | 9.0.0        |                                                                                                                                                                   |
| Node.js                         | 6.11.5       | [node-v6.11.5.pkg](https://nodejs.org/dist/v6.11.5/node-v6.11.5.pkg)                                                                                              |
| .NET Core                       | 2.0.2        | [dotnet-sdk-2.0.2-osx-x64.pkg](https://download.microsoft.com/download/7/3/A/73A3E4DC-F019-47D1-9951-0453676E059B/dotnet-sdk-2.0.2-osx-x64.pkg)                   |
| PowerShell Core                 | 6.0.0-beta.9 | [powershell-6.0.0-beta.9-osx.10.12-x64.pkg](https://github.com/PowerShell/PowerShell/releases/download/v6.0.0-beta.9/powershell-6.0.0-beta.9-osx.10.12-x64.pkg)   |
| Mono                            | 5.4.1.4      | [MonoFramework-MDK-5.4.1.4.macos10.xamarin.universal.pkg](https://dl.xamarin.com/MonoFrameworkMDK/Macx86/MonoFramework-MDK-5.4.1.4.macos10.xamarin.universal.pkg) |
| Xamarin.iOS                     | 11.4.0.93    | [xamarin.ios-11.4.0.93.pkg](https://dl.xamarin.com/MonoTouch/Mac/xamarin.ios-11.4.0.93.pkg)                                                                       |
| Xamarin.Mac                     | 4.0.0.93     | [xamarin.mac-4.0.0.93.pkg](https://dl.xamarin.com/XamarinforMac/Mac/xamarin.mac-4.0.0.93.pkg)                                                                     |
| Xamarin.Android                 | 8.1.0-21     | [xamarin.android-8.1.0-21.pkg](https://dl.xamarin.com/MonoforAndroid/Mac/xamarin.android-8.1.0-21.pkg)                                                            |
| Visual Studio for Mac (Preview) | 7.3.0.708    | [VisualStudioForMac-Preview-7.3.0.708.dmg](https://dl.xamarin.com/VsMac/VisualStudioForMac-Preview-7.3.0.708.dmg)                                                 |

#### Windows Dependencies

| Component                           | Version      | Download                                                                                                                                            |
| :---------------------------------- | :----------- | :-------------------------------------------------------------------------------------------------------------------------------------------------- |
| Visual Studio Preview (any edition) | 15.5.0       | [Download](https://www.visualstudio.com/vs/preview/) • _Ensure the Xamarin workload is selected when installing_                                    |
| .NET Core                           | 2.0.2        | [dotnet-sdk-2.0.2-win-x64.exe](https://download.microsoft.com/download/7/3/A/73A3E4DC-F019-47D1-9951-0453676E059B/dotnet-sdk-2.0.2-win-x64.exe)     |
| Node.js                             | 6.11.5       | [node-v6.11.5-x64.msi](https://nodejs.org/dist/v6.11.5/node-v6.11.5-x64.msi)                                                                        |
| NuGet CLI                           | 4.3.0        | [nuget.exe](https://dist.nuget.org/win-x86-commandline/v4.3.0/nuget.exe)                                                                            |
| Git                                 | 2.14.3       | [Git-2.14.3-64-bit.exe](https://github.com/git-for-windows/git/releases/download/v2.14.3.windows.1/Git-2.14.3-64-bit.exe)                           |
| 7-Zip                               | 17.01        | [7z1701-x64.msi](http://www.7-zip.org/a/7z1701-x64.msi)                                                                                             |

### Building

Ensure git submodules are up-do-date:

```bash
git submodule sync
git submodule update --recursive --init
```

Any edition of Visual Studio or Visual Studio for Mac can be used to develop,
build, and run Xamarin Workbooks by opening the top-level
`Xamarin.Interactive.sln` solution. The entire solution is shared on macOS
and Windows, so you will need to set the solution platform appropriately
in Visual Studio:

| OS      | Solution Platform | Solution Configuration           |
| :------ | ----------------- | -------------------------------- |
| macOS   | `macOS`           | `Debug` _(default)_ or `Release` |
| Windows | `Windows`         | `Debug` _(default)_ or `Release` |

It is recommended that your local builds use the default `Debug` solution
configuration.

Finally, building from the command line is straightforward on both
macOS and Windows. Unlike when building from Visual Studio, building
directly via `Build.proj` does _not_ require the solution platform
(`/p:Platform`) to be set manually.

```bash
msbuild Build.proj
```

#### `Build.proj` Targets

Our top-level `Build.proj` MSBuild project has a number of useful targets:

| Target | Description                                                                                                                                  |
| :----- | :------------------------------------------------------------------------------------------------------------------------------------------- |
| `Build` _(Default)_          | Perform a complete build of all projects                                                                               |
| `Clean`                      | Clean all projects                                                                                                     |
| `Package`                    | Builds a macOS `.pkg` or Windows `.msi` installer                                                                      |
| `TestRegressions`            | Runs the regression unit test suite                                                                                    |
| `UpdatePublicApiDefinitions` | Updates the API reference file with any changes in public API for the [Xamarin.Workbooks.Integration NuGet][our-nuget] |
| `UpdatePublicApiDocs`        | Performs an `mdoc update` of API documentation for `Xamarin.Interactive.dll`                                           |
| `AssemblePublicApiDocs`      | Performs an `mdoc assemble` of API documentation for `Xamarin.Interactive.dll`                                         |

#### Windows Nuances

If you want to build a `Release` build on Windows (for example, you want to
build an installer), you will need to build in a slightly different fashion.
First, make sure that you connect to a Mac build host via Visual Studio at
least once. You can do this by doing the following:

* Open Visual Studio
* Go to _Tools → Options → Xamarin → iOS Settings_
* Click "Find Xamarin Mac Agent"
* Select a Mac on your network, or add one by name
* Enter credentials when prompted

Once the connection completes, click OK to close all the dialogs. Then,
build the `Release` configuration by running the following:

```bash
msbuild Build.proj \
  /p:MacBuildHostAddress="<hostname-or-ip-of-your-mac>" \
  /p:MacBuildHostUser="<mac-username>" \
  /p:Configuration=Release /t:Build,Install
```

This is needed because the installer build now needs a zipped copy of the
Xamarin.iOS workbook app from the server. The `Xamarin.Workbooks.iOS` project
will do the build and copy automatically when a Mac build host is used. If you
are building in Debug, you can omit those properties unless you need the
Workbook app to be copied locally, in which case, include them there as well.

**Note:** the build will read properties from `Build/Local.props` as well,
for example:

```xml
<Project>
  <PropertyGroup>
    <MacBuildHostAddress>porkbelly</MacBuildHostAddress>
    <MacBuildHostUser>aaron</MacBuildHostUser>
  </PropertyGroup>
</Project>
```

## Contributing

This project welcomes contributions and suggestions. Most contributions require
you to agree to a Contributor License Agreement (CLA) declaring that you have
the right to, and actually do, grant us the rights to use your contribution.
For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether
you need to provide a CLA and decorate the PR appropriately (e.g., label,
comment). Simply follow the instructions provided by the bot. You will only
need to do this once across all repositories using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/)
or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any
additional questions or comments.

## Notices

### Telemetry

Official builds and releases of Xamarin Workbooks & Inspector from Microsoft
collect usage data and send it to Microsoft to help improve our products
and services. [Read our privacy statement to learn more](https://go.microsoft.com/fwlink/?LinkID=824704).

Users may opt out of telemetry and usage data collection from the _Preferences_
dialog.

_Non-Microsoft builds do not enable telemetry collection at all._

### Third Party Code

Xamarin Workbooks & Inspector incorporates open source code from external
projects. See [ThirdPartyNotices.txt](ThirdPartyNotices.txt) for attribution.

[our-nuget]: https://www.nuget.org/packages/Xamarin.Workbooks.Integration
[macbuildstatus]: https://devdiv.visualstudio.com/_apis/public/build/definitions/0bdbc590-a062-4c3f-b0f6-9383f67865ee/6539/badge "macOS Build Status"
[winbuildstatus]: https://devdiv.visualstudio.com/_apis/public/build/definitions/0bdbc590-a062-4c3f-b0f6-9383f67865ee/6563/badge "Windows Build Status"