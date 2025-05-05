# Example Flutter

Just a simple Flutter app, containing couple of routes and nav between them for a simple showcase. The main point of this repo is to give some basic understanding of what it takes to setup vscode and Flutter dev environment, without the need of AndroidStudio or MS VisualStudio - both coming with payed license once you decide to go more than hobby. Of course they have their great tools and UI, but for simple application development, most can be omit. 

## Development (VSCode - Android)

1. Install [Flutter Extensions](https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter)
2. Download and install [Flutter SDK](https://docs.flutter.dev/release/archive?tab=windows)
3. Download and install [Android CLI Tools](https://developer.android.com/studio)

> NOTE: use a folder structure like this `/{somewhere}/android/sdk/cmdline-tools/latest` - apparently the .execs files are 'sensitive' to location...

4. Add to environment PATH for both Flutter SDK and Android SDK Tools `/bin` folders
5. Use Android SDKManager to install a few tools

```sh
// setup the root folder for managing the sdk files
sdkmanager --sdk_root=/{somewhere}/android/sdk

// install android platform (to run onto)
sdkmanager --install 'platforms;android-34' 

// install android build-tools (to build the app)
sdkmanager --install 'build-tools;34.0.0'

// install emulator (to simulate, install & run the app into)
sdkmanager --install 'emulator'

sdkmanager --install 'platform-tools'
```

6. Configure flutter

```sh
// to use your android SDK
flutter config --android-sdk 'C:/dev/android/sdk/'

// read & accept the license agreements on the installed tools/platforms from above
flutter doctor --android licenses

// run diagnostics on your setup - if all went well, you should see all green, except VisualStudio and Android Studio not installed - we don't need those.
flutter doctor -v
```

6. Create a project via CMD pallet in VSCode - Flutter: New Project

> NOTE: at this point your project by default (on Windows machine) will preselect Windows as the device to run the app, which will cause an error (unless you have VisualStudio installed with Android Toolchain). Since we are using VSCode, we can simply change the target device to Chrome (or go to next step using an emulator).

7. Prep emulator

```sh
// install an image (blueprint for the phone OS)
sdkmanager --install 'system-images;android-34;google_apis_playstore;x86_64'

// create an emulator with Name (-n), Image (-k) and DeviceFeatures (-d)
avdmanager -s create avd -n 'Google_Pixel_7_Pro' -k "system-images;android-34;google_apis_playstore;x86_64" -d 32

// launch
flutter emulator --launch Google_Pixel_7_Pro
```

8. Run project (via [main](./test_app/lib/main.dart) entry point) 

> NOTE: this will build an .apk (if you are working with android), install it on the target device environment and open up the application.

```sh
cd test_app
flutter run
```

> NOT: this will use the first available AVD, but if you want to specifiy a target one to build and install the apk use `flutter devices` and use the name of it like this `flutter run -d emulator-5554` for example

