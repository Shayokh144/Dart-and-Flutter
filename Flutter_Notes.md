# Flutter

## Introduction

- As a cross-platform framework, Flutter most closely resembles React Native. Both allow for a reactive and declarative style of programming. Unlike React Native, however, Flutter doesn’t need to use a JavaScript bridge, which improves app startup times and overall performance. Dart achieves this by using **Ahead-Of-Time (AOT)** compilation.

- Dart can also use `Just-In-Time (JIT)` compilation. JIT compilation with Flutter improves the development workflow by allowing a `hot reload` capability to refresh the UI during development without the need for an entirely new build.

## Setting up Flutter

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