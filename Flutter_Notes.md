# Flutter

## Introduction

- As a cross-platform framework, Flutter most closely resembles React Native. Both allow for a reactive and declarative style of programming. Unlike React Native, however, Flutter doesn’t need to use a JavaScript bridge, which improves app startup times and overall performance. Dart achieves this by using **Ahead-Of-Time (AOT)** compilation.

- Dart can also use `Just-In-Time (JIT)` compilation. JIT compilation with Flutter improves the development workflow by allowing a `hot reload` capability to refresh the UI during development without the need for an entirely new build.

## Setting up Flutter on Mac

- [Installation](https://docs.flutter.dev/get-started/install)
- Follow commands from above lin, don't extract the sdk by double click. Use provided command onn the link instead.
-  [Permanently add Flutter to your path](https://docs.flutter.dev/get-started/install/macos#update-your-path)
- After running `flutter doctor` if you find error related `android plugin`, install android studio then run the command again.

- Now if you get error like this:
```
Android sdkmanager not found. Update to the latest Android SDK and ensure that the cmdline-tools are installed to resolve
this.
```
- [Follow this answer](https://stackoverflow.com/a/60529140/4245112)
- Now run `flutter doctor --android-licenses`
- Now run `flutter doctor`

## Create a flutter project

- Run `flutter create my_app`
- Run `cd my_app`
- Open iPhone Simulator by running: `open -a Simulator`
- Run `flutter run`
- [Run on actual iPhone](https://docs.flutter.dev/get-started/install/macos#deploy-to-ios-devices)
- [Run on android](https://docs.flutter.dev/get-started/install/macos#set-up-your-android-device)


## Using new package/ library
- All library and packages for Dart and Flutter can be found [here](https://pub.dev/)
- For example we will search a library named `http`, this will be used to send http request and receive response
- Search `http` in the site, copy it's name with version from copy icon
- In the `Dependency` section of `pubspec.yaml` paste it under `cupertino_icons: ^1.0.2`
- Run `flutter pub get` from terminal


## Flutter app anatomy
- Everythin on the screen of a flutter app is `Widget`
- `Scaffold` is a built-in widget represent an empty screen
- `Row, column, container, appbar, Network Image` are some of the built-in widget

## Useful commands
- Open an iOS Simulator using UDID 

`open -a Simulator --args -CurrentDeviceUDID E8F3E058-D58E-4594-9BE9-7CD16DA98066
`

- Get available list of simulator with udid

`xcrun simctl list`

