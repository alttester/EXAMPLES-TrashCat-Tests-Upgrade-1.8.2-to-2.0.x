The main includes test cases and setup procedures for executing tests using AltTester SDK 1.8.2. These tests are designed specifically for the TrashCat build mentioned in the following lines. If you're looking for tests upgraded to version 2.0.0, please check the [TestsFor2.0.0 branch](https://github.com/alttester/EXAMPLES-TrashCat-Tests/tree/TestsFor2.0.0).

## Prerequisite

1. Download and install [.NET SDK](https://dotnet.microsoft.com/en-us/download)
2. Have a game [instrumented with AltTester Unity SDK](https://alttester.com/app/uploads/AltTester/TrashCat/TrashCatStandAlone182FNoTutorial.zip).
3. Have [AltTester Desktop app](https://github.com/alttester/AltTester-Unity-SDK/releases) installed (to be able to inspect game)
- For SDK v 1.8.2 => need to use AltTester Desktop 1.5.1 (at least)
- For SDK v 2.0.0 => need to use AltTester Desktop 2.0.0
4. Add AltTester package:
```
dotnet add package AltTester-Driver --version 1.8.2
```

### Workaround for being able to use SDK 1.8.2 installed as package in project:
- get `altwebsocket-sharp.dll` from [here](https://github.com/alttester/AltTester-Unity-SDK/tree/development/Assets/AltTester/Runtime/3rdParty/websocket-sharp/netstandard2.0) and put in project's bin\Debug\net7.0

this was necessary due to currently open [issue](https://github.com/alttester/AltTester-Unity-SDK/issues/1192)

### Specific for running on Android from Windows
5. Download and install [ADB for Windows](https://dl.google.com/android/repository/platform-tools-latest-windows.zip)
6. Enable Developers Options on mobile device [more instructions here](https://www.xda-developers.com/install-adb-windows-macos-linux/)

# Setup for running on mobile device
For Android, here is a specific [build instrumented with AltTester SDK](https://alttester.com/app/uploads/AltTester/TrashCat/TrashCatAndroid182FNoTutorial.zip).

1. Make sure mobile device is connected via USB, execute:

```
adb devices
```

2. On mobile device: allow USB Debugging access (RSA key fingerprint from computer)

3. Uninstall the app from the device

```
adb uninstall com.Altom.TrashCat
```

4. Install the app on the device

```
adb install TrashCat.apk
```

# Run tests manually (with [dotnet CLI](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-test))

1. [Optional to do manually] Setup ADB port forwarding (this can also be done in code in Setup and Teardown)

```
adb forward --remove-all
```

```
adb forward tcp:13000 tcp:13000
```

2. Launch game

```
adb shell am start -n com.Altom.TrashCat/com.unity3d.player.UnityPlayerActivity
```

3. Execute all tests:

```
dotnet test
```

4. Kill app
```
adb shell am force-stop com.Altom.TrashCat
```

! **When running v 1.8.2 make sure to have the AltTester Desktop App closed, otherwise the test won't be able to connect to proper port.**

### Run all tests from a specific class / file

```
dotnet test --filter <test_class_name>
```

### Run only one test from a class

```
dotnet test --filter <test_class_name>.<test_name>
```

