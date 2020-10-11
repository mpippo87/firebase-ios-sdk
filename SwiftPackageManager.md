# Swift Package Manager for Firebase **Beta**

## Introduction

Starting with the 6.31.0 release, Firebase supports installation via [Swift
Package Manager](https://swift.org/package-manager/) in Beta status.


## Limitations

- Requires Xcode 12.
- Analytics requires clients to add `-ObjC` linker option.
- Analytics is only supported for iOS and cannot be used in apps that support other platforms.
- Messaging, Performance, Firebase ML, and App Distribution are not initially available.
- watchOS support is not initially available.

## Installation

If you've previously used CocoaPods, remove them from the project with `pod deintegrate`.

### In Xcode

Install Firebase via Swift Package Manager:

<img src="docs/resources/SPMAddPackage.png">

Select the Firebase GitHub repository - `https://github.com/firebase/firebase-ios-sdk.git`:

<img src="docs/resources/SPMChoose.png">

Select the beta branch.

Note: Starting with the 6.31.0 release, the versions are specified
in a format like 6.34-spm-beta. We won't support standard repository
versioning until later in the beta or with general availability of the SPM
distribution.

<img src="docs/resources/SPMSelect.png">

Choose the Firebase products that you want installed in your app.

<img src="docs/resources/SPMProducts.png">

If you've installed FirebaseAnalytics, add the `-ObjC` option to `Other Linker Flags`
in the `Build Settings` tab for each target in the project.

If you're using FirebaseAnalytics, Xcode 12.0, and have an issue with
device installation or archive uploading, see the workaround at
https://github.com/firebase/firebase-ios-sdk/issues/6472#issuecomment-694449182.

<img src="docs/resources/SPMObjC.png">

### Alternatively, add Firebase to a `Package.swift` manifest

To integrate via a `Package.swift` manifest instead of Xcode, you can add
Firebase to your dependencies array of your package with:

```
dependencies: [
  // Substitute X.Y with the version of Firebase you want.
  .package(name: "Firebase",
           url: "https://github.com/firebase/firebase-ios-sdk.git",
           .branch("X.Y-spm-beta")),

  // Any other dependencies you have...
],
```

Then in any target that depends on a Firebase product, add it to the `dependencies`
array of that target:

```
.target(
    name: "MyTargetName",
    dependencies: [
      // The product name you need. In this example, FirebaseAuth.
      .product(name: "FirebaseAuth", package: "Firebase"),
    ]
),
```

## Questions and Issues

Please provide any feedback via a [GitHub
Issue](https://github.com/firebase/firebase-ios-sdk/issues/new?template=bug_report.md).

See current open Swift Package Manager issues
[here](https://github.com/firebase/firebase-ios-sdk/labels/Swift%20Package%20Manager).
