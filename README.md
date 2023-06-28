The `TestsFor2.0.0` branch includes test cases and setup procedures for executing tests using AltTester SDK 2.0.0. These tests are designed specifically for the TrashCat build mentioned in the following lines. If you're looking for tests for AltTester version 1.8.2, please check the [main branch](https://github.com/alttester/EXAMPLES-TrashCat-Tests/tree/main).

## Prerequisite

1. Download and install [.NET SDK](https://dotnet.microsoft.com/en-us/download)
2. Have a build [instrumented with AltTester SDK 2.0.0](https://alttester.com/docs/sdk/pages/get-startedhtml#instrument-your-game-with-alttester-unity-sdk).
3. Have [AltTester Desktop app, 2.0.0](https://alttester.com/alttester/) installed (to be able to inspect game).
- For SDK v 2.0.0 => need to use AltTester Desktop 2.0.0
4. Add AltTester package:
```
dotnet add package AltTester-Driver --version 2.0.0
```

### Specific for running on Android from Windows
5. Download and install [ADB for Windows](https://dl.google.com/android/repository/platform-tools-latest-windows.zip)
6. Enable Developers Options on mobile device [more instructions here](https://www.xda-developers.com/install-adb-windows-macos-linux/)

# Setup for running on mobile device

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
! **When running v2.0.0 make sure to have the AltTester Desktop App running**

1. [Optional to do manually] Setup ADB reverse port forwarding (this can also be done in code in Setup and Teardown)

```
adb forward --remove-all
```

```
adb reverse tcp:13000 tcp:13000
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


### Run all tests from a specific class / file

```
dotnet test --filter <test_class_name>
```

### Run only one test from a class

```
dotnet test --filter <test_class_name>.<test_name>
```

