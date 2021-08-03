# bitcode-local-swift-package-issue

1. Given an iOS app with a watch app Xcode project.
2. The watch app has bitcode explicitly enabled with `ENABLE_BITCODE=YES`.
3. A local Swift package is used as a library in the watch app.
4. This leads to a bitcode warning saying that "all bitcode will be dropped because the package was built without bitcode" when building the app on simulator builds.

## Actual result
Building the app on simulator builds gives the following bitcode warning in the `Built target SampleWatchApp Extension: Link SampleWatchApp Extension (arm64)` step:


> ld: warning: all bitcode will be dropped because '/Users/username/Library/Developer/Xcode/DerivedData/SampleApp-egrqmpcsrjdhaxfjdiwqjeljghpq/Build/Products/Debug-watchsimulator/LocalSwiftPackage.o' was built without bitcode. You must rebuild it with bitcode enabled (Xcode setting ENABLE_BITCODE), obtain an updated library from the vendor, or disable bitcode for this target. 

## Expected result
The app builds without warnings on simulator builds (like on physical device builds) when a local swift package is used in the watch app.

## Steps to reproduce with the sample project
1. Select the "SampleApp" scheme and an iPhone simulator as the run destination.
2. Build the app.  
--> This leads to the bitcode build warning.

3. cross check: Select a physical device as the run destination. (Configure Signing & Capabilities for the targets, if needed.)  
--> The bitcode build warning does not occur.

## Environment
- iOS 14.5
- watchOS 7.4
- Swift tools version 5.3
- Xcode 12.5.1 (12E507)
