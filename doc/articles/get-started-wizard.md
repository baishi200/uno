# Welcome to Uno Platform!

## Please read important installation information below.

Congratulations, you've just created a new project using the [Uno Platform](https://platform.uno/) project templates!

* You can give the [Single Page app getting started guide](https://platform.uno/docs/articles/getting-started-tutorial-1.html) a try
* Next you can try our [Bug Tracker sample walk-through](https://platform.uno/docs/articles/getting-started-tutorial-2.html)
* More advanced examples in our [Uno.Samples repository](https://github.com/unoplatform/uno.samples)
* Fork a fully-fledged [Ch9 application and source code ](https://platform.uno/code-samples/#ch9)
* You can find detailed documentation on Uno topics [on our web site](https://platform.uno/docs/articles/intro.html).

## Common Issues
The Uno Platform features and support is constantly evolving, but you may encounter some of the  issues below while building your application.

### XAML Hot Reload for the UWP head may not work properly in Visual Studio 2019 16.7 and earlier
The [XAML Hot Reload](https://docs.microsoft.com/en-us/visualstudio/xaml-tools/xaml-hot-reload?view=vs-2019) feature [does not work in Visual Studio 2019 16.7](https://developercommunity.visualstudio.com/content/problem/996417/xaml-hot-reload-hot-reload-is-not-working-in-share.html) and earlier for Uno projects. This will be fixed in 16.8 and later.

### The XAML editor shows `The type 'page' does not support direct content` message
XAML Intellisense [is not working properly](https://developercommunity.visualstudio.com/content/problem/587980/xaml-intellisense-does-not-use-contentpropertyattr.html) in Visual Studio when the active project is not the UWP one. 

To work around this issue, close all XAML editors, open a C# file and select 'UWP' in the top left drop-down list of the text editor sector. Once selected, re-open the XAML file.

### The XAML editor may be empty
The XAML editor may be empty when the active editor project is not UWP.

To work around this issue, close all XAML editors, open a C# file and select 'UWP' in the top left drop-down list of the text editor sector. Once selected, re-open the XAML file.

### `InitializeComponent` or `x:Name` variable is not available in code-behind
Visual Studio 16.7 and earlier versions [do not refresh the intellisense cache ](https://developercommunity.visualstudio.com/content/problem/588021/the-compile-itemgroup-intellisense-cache-is-not-re.html)properly, causing variables to be incorrectly defined.

To fix this issue, build your project once, close the solution and reopen it.

### Event handler cannot be added automatically

Event handlers [cannot be automatically](https://github.com/unoplatform/uno/issues/1348#issuecomment-520300471) added using the XAML editor. 

A workaround is to use the [`x:Bind` to events feature](features/windows-ui-xaml-xbind.md#examples). This feature allows to use a simpler syntax like `<Button Click="{x:Bind MyClick}" />` and declare a simple method `private void MyClick() { }` in the code-behind.

### Runtime error `No parameterless constructor defined for XXXX`
This error is generally caused by some missing [IL Linker](https://github.com/mono/linker/tree/master/docs) configuration on WebAssembly. You may need to add some of your application assemblies in the LinkerConfig.xml file of your project. You can find [additional information in the documentation](features/using-il-linker-webassembly.md).

### The path may be too long
The project may fail to build if the path of any file in the project is [too long](https://docs.microsoft.com/en-us/windows/win32/fileio/maximum-file-path-limitation).

To work around this issue, either:
- Move the project to a shorter root path, or
- Enable Long Path support in Windows 10 by executing this:
```
reg ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem /v LongPathsEnabled /t REG_DWORD /d 1
```

### "Missing value for TargetPlatformWinMDLocation property" when adding a project reference
This issue is caused by [VS 2019 support for SDK-Style projects](https://developercommunity.visualstudio.com/content/problem/1170010/missing-value-for-targetplatformwinmdlocation-prop.html).

To add a reference change the list of `<TargetFramework>` to place `netstandard2.0` at the first position, in the project you are trying to adding the reference to.

### Build fails with `error : Error reading response`
In general, this error happens when the XAML parser detects a syntax error. Fixing the error generally fixes the build.

This error may happen occasionally without any explicit error message, rebuilding the project may fix the issue.

### System.DllNotFoundException: Gtk: libgtk-3-0.dll

When running the Skia.GTK project head, the following error may happen:

```
Unhandled exception. System.TypeInitializationException: The type initializer for 'Gtk.Application' threw an exception.
---> System.DllNotFoundException: Gtk: libgtk-3-0.dll, libgtk-3.so.0, libgtk-3.0.dylib, gtk-3.dll
```

On Windows, you will need to install the [GTK+3 runtime](https://github.com/tschoonj/GTK-for-Windows-Runtime-Environment-Installer/releases). **Make sure to restart Visual Studio** for the changes to be used by Visual Studio.
On Linux, you'll need to follow the [Uno Platform](get-started-with-linux.md#setting-up-for-linux) setup instructions.
On macOS, you'll need to follow the [Uno Platform](get-started-with-vsmac.md) setup instructions.
