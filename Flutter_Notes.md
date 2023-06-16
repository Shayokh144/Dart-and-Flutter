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

## Flutter Widgets
- A Flutter app is itself a widget.
- Widgets are classes used to build UIs. They are used for both layout and UI elements.
- In Flutter, almost everything is a widget—even layout models are widgets. The images, icons, and text that you see in a Flutter app are all widgets. But things you don’t see are also widgets, such as the rows, columns, and grids that arrange, constrain, and align the visible widgets.
- All layout widgets have either of the following:
	- A `child` property if they take a single child—for example, Center or Container
	- A `children` property if they take a list of widgets—for example, Row, Column, ListView, or Stack.
- `BuildContext` is used to provide the position where the widget will sit in the element tree
- 3 types of widget:
	- Stateless widget
	- Statefull widget
	- Inherited Widget

## Widget Constraint
- A widget gets its own constraints from its parent. A constraint is just a set of 4 doubles: a minimum and maximum width, and a minimum and maximum height.
- Then the widget goes through its own list of children. One by one, the widget tells its children what their constraints are (which can be different for each child), and then asks each child what size it wants to be.
- Then, the widget positions its children (horizontally in the x axis, and vertically in the y axis), one by one. And, finally, the widget tells its parent about its own size (within the original constraints, of course).
- A widget can decide its own size only within the constraints given to it by its parent. This means a widget usually can’t have any size it wants.

### Inherited Widget
- Used to share state between child widgets
- [Resource](https://www.youtube.com/watch?v=utrvu-eow6U)

### Container 
- Container is a widget class that allows you to customize its child widget. 
- Use a Container when you want to add padding, margins, borders, or background color, to name some of its capabilities.


## Flutter iOS App CD to Testflight

- First run 

		flutter build ipa

- If you have different schemes run:

		flutter build ipa --flavor SCHEME_NAME
- This may generate `provision profile` related error, to solve this:
	- Create app using a bundle id in Appstore connect
	- Add that bundle id in `Xcode` -> `Signing And Capabilities` -> `Bundle Identifier`
	- Click `Automatically manage signing`
- Now try `flutter build ipa --flavor SCHEME_NAME` command again. This time it should work and ipa should be generated it this path: `PROJECT_ROOT/build/ios/ipa/*.ipa`
- Go to app store connect, find created apps, then click `TestFlight` tab. Click `Internal Testing` to create tester group and add emails of people who wants to run Testflight build.
- Create provision profile using bundle id for type `Development` and `AppStore`(for TestFlight upload)
- Create a gem file which contains at least: `gem "fastlane"`
- You need to add `gem "cocoapods"` if you are using cocoapods.
- Install bundler by running: `gem install buldler`
- Now from the same directory where your `Gem file` is stored, run: `bundle install`
- Now run `fastlane init` and configure accordingly
- Now run `fastlane match appstore` and `fastlane match development` if these commands are successful we are good to go. 	
- Learn about [fastlae match from here](https://youtu.be/Edr88s5YlH4)
- Run `fastlane init` to create `Fastfile`
- Create lane like below:

```Ruby
  desc 'Build and upload Flutter Staging app to Test Flight'
  lane :futter_build_and_upload_testflight_staging_app do
    #bump_build
    build_app(
      scheme: Constants.SCHEME_NAME_STAGING,
      output_name: Constants.PRODUCT_NAME_STAGING,
      skip_build_archive: true,
      archive_path: "../build/ios/archive/Runner.xcarchive" 
      # this archive is generated by flutter build ipa --flavor SCHEME_NAME this command
    )
    #upload_build_to_testflight
    api_key = app_store_connect_api_key(
      key_id: ENV['APP_STORE_CONNECT_API_KEY_KEY_ID'],
      issuer_id: ENV['APP_STORE_CONNECT_API_KEY_ISSUER_ID'],
      key_content: ENV['APP_STORE_CONNECT_API_KEY_IS_KEY_CONTENT_BASE64'],
      is_key_content_base64: true,
      in_house: true
    )
    pilot(api_key: api_key)
  end
```	
- Now run this lane to upload in testflight
- Follow [this PR](https://github.com/nimblehq/ic-flutter-taher-toby/pull/51) for more details

## Learn Riverpod
### why riverpod
Riverpod is very versatile, and you can use it to:

- catch programming errors at compile-time rather than at runtime
- easily fetch, cache, and update data from a remote source
- perform reactive caching and easily update your UI
- depend on asynchronous or computed state
- create, use, and combine providers with minimal boilerplate code
- dispose the state of a provider when it is no longer used
- write testable code and keep your logic outside the widget tree
- Riverpod implements well-defined patterns for retrieving and caching data, so you don't have to reimplement them.
- `Riverpod is compile-safe since all providers are declared globally and can be accessed anywhere`. This means that you can create providers to hold your application state and business logic outside the widget tree.
- since Riverpod is a reactive framework, it makes it easier to only rebuild your providers and widgets when needed.
- [small article](https://medium.com/@FlutterTech/a-masterclass-in-flutter-state-management-riverpod-b24f5992f646)
- [resource](https://resocoder.com/2022/04/22/riverpod-2-0-complete-guide-flutter-tutorial/)
- [more resource](https://codewithandrea.com/articles/flutter-state-management-riverpod/)
- [How to handle loading and error states with StateNotifier & AsyncValue in Flutter](https://codewithandrea.com/articles/loading-error-states-state-notifier-async-value/)

## Navigation with navigator
- For simple navigation we can use Navigator:
- Push a new screen
```Dart
Navigator.push(
    context,
    MaterialPageRoute(builder: (context) => const NewScreenWidget()),
  );
```
- Pop current screen
```Dart
Navigator.pop(context);
```
- For named argument we can use  `Navigator.pushNamed()` but it is not recommended to use, need to use `GoRoute` instead.
- Deeplink for [Android](https://docs.flutter.dev/cookbook/navigation/set-up-app-links)
- Deeplink for [iOS](https://docs.flutter.dev/cookbook/navigation/set-up-universal-links)
## Learn Go_Router
- User for navigation inside the app
- [resource](https://blog.codemagic.io/flutter-go-router-guide/)

## Useful commands
- Open an iOS Simulator using UDID 

`open -a Simulator --args -CurrentDeviceUDID E8F3E058-D58E-4594-9BE9-7CD16DA98066
`

- Get available list of simulator with udid

`xcrun simctl list`

- Run flutter app with specific scheme like staging or production

`flutter run --flavor staging`

- Run build-runner command

`fvm flutter packages pub run build_runner build --delete-conflicting-outputs`
