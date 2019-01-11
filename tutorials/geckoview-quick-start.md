
# GeckoView Contributor Quick Start Guide

This is a guide for developers who want to contribute to the GeckoView project. If you want to get started using GeckoView in your app then you should refer to the [wiki](https://wiki.mozilla.org/Mobile/GeckoView#Get_Started).

You may also be interested in how to get up and running with [Firefox For Android](https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Build_Instructions/Simple_Firefox_for_Android_build).

## Get set up with Mozilla Central

The GeckoView codebase is part of the main Firefox tree and can be found in `mozilla-central`. You will need to get set up as a contributor to Firefox in order to contribute to GeckoView. To get set up with `mozilla-central`, follow the [Quick Start Guide for Git Users](mc-quick-start.md), or the [Contributing to the Mozilla code base](https://developer.mozilla.org/docs/Mozilla/Developer_guide/Introduction) guide on [MDN](https://developer.mozilla.org/) for Mercurial users.

Once you have a copy of `mozilla-central`, you will need to build GeckoView.

## Bootstrap Gecko
Bootstrap configures everything for GeckoView and Fennec development.

* Ensure you have `mozilla-central` checked out. If this is the first time you are doing this, it may take some time.

```bash
git checkout central/default
```
If you are on a mac, you will need to have the Xcode build tools installed. You can do this by either [installing Xcode](https://developer.apple.com/xcode/) or installing only the tools from the command line by running `xcode-select --install` and following the on screen instructions. Use the ` --no-interactive` argument to automatically accept any license agreements.

```bash
./mach bootstrap [ --no-interactive]
```
* Choose option `4. Firefox for Android` for GeckoView development. This will give you a version of Gecko configured for Android that has not bundled the native code into embedded libraries so you can amend the code.
* Say Y to all configuration options
* Once `mach bootstrap` is complete it will tell you to copy and paste some configuration into your `mozconfig` file. The `mozconfig` file can be found in the root of your `gecko` repo - or create a file called `mozconfig` if it does not exist. Check that the correct value is associated with the `--target` argument as this may not correctly match your setup. Your `mozconfig` should read something like this:

```bash
mk_add_options MOZ_OBJDIR=../objdir-android-opt

# Build Firefox for Android:
ac_add_options --enable-application=mobile/android
ac_add_options --target=<your target architecture>

# With the following java and javac:
ac_add_options --with-java-bin-path="/Library/Java/Home/bin"

# With the following Android SDK and NDK:
ac_add_options --with-android-sdk="$HOME/.mozbuild/<your-sdk>"
ac_add_options --with-android-ndk="$HOME/.mozbuild/android-ndk-r17b"

```
* Configure your build.

```bash
./mach configure
```
## Build from the command line

In order to pick up the configuration changes we just made we need to build from the command line and package the app.

```bash
./mach build
./mach package
```
## Build Using Android Studio

* Install [Android Studio](https://developer.android.com/studio/install).
* Disable Instant Run. This is because Fennec and the Geckoview Example app cannot deploy with Instant Run on.
  * Select Android Studio > Preferences from the menu bar
  * Navigate to Build, Execution, Deployment > Instant Run.
  * Uncheck the box that reads `Enable Instant Run to hot swap code/resource changes on deploy`.
  ![alt text](assets/DisableInstantRun.png "Disable Instant Run")
* Choose File->Open from the toolbar
* Navigate to <path to gecko>/mobile/android/geckoview and click "Open"
* Click yes if it asks if you want to use the gradle wrapper.
* Wait for the project to index and gradle to sync. Once synced, the workspace will reconfigure to display the different projects.
  * annotations contains custom annotations used inside GeckoView and Fennec.
  * app is Fennec - Firefox for Android. Here is where you will find code specific to that app.
  * geckoview is the GeckoView project. Here is all the Java files related to GeckoView
  * geckoview_example is an example browser built using GeckoView.
  * omnijar contains the parts of Gecko and GeckoView that are not written in Java or Kotlin
  * thirdparty contains third party code that Fennec and GeckoView use.
  ![alt text](assets/GeckoViewStructure.png "GeckoView Structure")

Now you're set up and ready to go.

## Performing a bug fix

One you have got GeckoView building and running, you will want to start contributing. There is a general guide to [Performing a Bug Fix for Git Developers](contributing-to-mc.md) for you to follow. To contribute to GeckoView specifically, you will need the following additional information.

### Updating the changelog and API documentation

If the patch that you want to submit changes the public API for GeckoView, you must ensure that the API documentation is kept up to date. To check whether your patch has altered the API, run the following command.

```bash
./mach android api-lint
```

The output of this command will inform you if any changes you have made break the existing API. Review the changes and, if they are correct, update your api.txt to conform to your changed by running:

```bash
./gradlew apiUpdateFileWithGeckoBinariesDebug
```

After updating the API documentation, rerun `mach android api-lint`. This will then provide you with a changelog hash number. Open `mobile/android/geckoview/src/main/java/org/mozilla/geckoview/doc-files/CHANGELOG.md` and make the following changes.

1. Under the heading for the next release version, add a new entry for the changes that you are making to the API, along with links to any relevant files. i.e.

  ```
  - Added methods for each setting in [`GeckoSessionSettings`][66.3] 
  [66.3]: ../GeckoSessionSettings.html
  ```

2. Copy and paste the changelog hash from the api-lint output against the `[api-version]` entry at the bottom of the file.

### Submitting to the `try` server

It is advisable to run your tests before submitting your patch. You can do this using Mozilla's `try` server. To submit a GeckoView patch to `try` before submitting it for review, type:
```bash
./mach try fuzzy -q "android"
```

This will run all of the Android test suite. If your patch passes on `try` you can be (fairly) confident that it will land successfully after review.

### Tagging a reviewer

When submitting a patch to Phabricator, if you know who you want to review your patch, put their Phabricator handle against the `reviewers` field. 

If you don't know who to tag for a review in the Phabricator submission message, leave the field blank and, after submission, follow the link to the patch in Phabricator and scroll to the bottom of the screen until you see the comment box. 
  * Select the `Add Action` drop down and pick the `Change Reviewers` option.
  * In the presented box, add `geckoview-reviewers`. Selecting this group as the reviewer will notify all the members of the GeckoView team there is a patch to review.
  * Click `Submit` to submit the reviewer change request.

## Include GeckoView as a dependency

If you want to include a development version of GeckoView as a dependency inside another app, you must link to a local copy. There are two ways of doing this, publishing GeckoView to a local Maven repository (recommended), or linking to a local archive/

### Publish to a local repository

Publish GeckoView to your local maven by running

```bash
./gradlew geckoview:publishWithGeckoBinariesDebugPublicationToMavenLocal
```

* The binary will have been published to a repo found in `~/.m2`. Run the following command to figure out the name of the artifcat:

```bash
$ tree ~/.m2/repository/org/mozilla/geckoview
```
* Make a note of the name of your artifact. Update your gradle file to point to the dependency and link to your local repository.

```gradle
dependencies {
    // ...
    armImplementation "geckoview-nightly-armeabi-v7a-65.0.20181128102620"    
    // ...
}

// ...

repositories {
  //...
  mavenLocal()
  //..
}
```

### Archive GeckoView

```bash
./mach android archive-geckoview
```

This should create a file named geckoview-*.aar in your build output folder (MOZ_OBJDIR):

```bash
ls <your-output-directory>/gradle/build/mobile/android/geckoview/outputs/aar
geckoview-official-withGeckoBinaries-noMinApi-release.aar
```

Then all you need to do is point to the AAR in your gradle file.

```gradle
repositories {
    // ...

    flatDir(
        name: 'localBuild',
        dirs: '<absolute path to AAR>'
    )
}
// ...
dependencies {
    // ...

    // armImplementation "org.mozilla:geckoview-nightly-armeabi-v7a:60.0a1"
    armImplementation (
            name: 'geckoview-official-withGeckoBinaries-noMinApi-release',
            ext: 'aar'
    )
    x86Implementation "org.mozilla:geckoview-nightly-x86:60.0a1"
    
    // ...
}
```


## Next Steps

- Get started with [Native Debugging](native-debugging.md)