---
layout: default
title: Get Started with GeckoView
nav_order: 2 
summary: How to use GeckoView in your Android app.
tags: [GeckoView,Gecko,mozilla,android,WebView,mobile,mozilla-central,setup,quick start]
---

_Building a browser? Check out [Android Components](https://mozilla-mobile.github.io/android-components/), our collection of ready-to-use support libraries!_

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Configure Gradle

You need to add or edit four stanzas inside your module's `build.gradle` file.

**1. Set the GeckoView version**

_Like Firefox, GeckoView has three release channels: Stable, Beta, and Nightly. Browse the [Maven Repository](https://maven.mozilla.org/?prefix=maven2/org/mozilla/geckoview/) to see currently available builds._

```groovy
ext {
    geckoviewChannel = "nightly"
    geckoviewVersion = "64.0.20180927100037"
}
```

**2. Add Mozilla's Maven repository**
```groovy
repositories {
    maven {
        url "https://maven.mozilla.org/maven2/"
    }
}
```

**3. Configure build flavors**

_Note: Until we resolve [Bug 1508976](https://bugzilla.mozilla.org/show_bug.cgi?id=1508976), you must configure a separate build variant for each CPU architecture.__

```groovy
android {
    // ...

    // Note: compileOptions is only required for minSdkVersion < 24
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }

    flavorDimensions "abi"

    productFlavors {
        x86     { dimension "abi" }
        x86_64  { dimension "abi" }
        arm     { dimension "abi" }
        aarch64 { dimension "abi" }
    }
}
```

**4. Add GeckoView Implementations**

```groovy
dependencies {
    // ...

    x86Implementation     "org.mozilla.geckoview:geckoview-${geckoviewChannel}-x86:${geckoviewVersion}"
    x86_64Implementation  "org.mozilla.geckoview:geckoview-${geckoviewChannel}-x86_64:${geckoviewVersion}"
    armImplementation     "org.mozilla.geckoview:geckoview-${geckoviewChannel}-armeabi-v7a:${geckoviewVersion}"
    aarch64Implementation "org.mozilla.geckoview:geckoview-${geckoviewChannel}-arm64-v8a:${geckoviewVersion}"
}
```

## Add GeckoView to a Layout

Inside a layout `.xml` file, add the following:

```xml
<org.mozilla.geckoview.GeckoView
    android:id="@+id/geckoview"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent" />
```

## Initialize GeckoView in an Activity

**1. Import the GeckoView classes inside an Activity:**

```java
import org.mozilla.geckoview.GeckoRuntime;
import org.mozilla.geckoview.GeckoSession;
import org.mozilla.geckoview.GeckoView;
```

**2. In that activity's <code>onCreate</code> function, add the following:**

```java
GeckoView view = findViewById(R.id.geckoview);
GeckoSession session = new GeckoSession();
GeckoRuntime runtime = GeckoRuntime.create(this);

session.open(runtime);
view.setSession(session);
session.loadUri("about:buildconfig"); // Or any other URL...
```

## You're done!

Your application should now load and display a webpage inside of GeckoView.

To learn more about GeckoView's capabilities, review GeckoView's [JavaDoc](https://mozilla.github.io/geckoview/javadoc/mozilla-central/) or the [reference application](https://searchfox.org/mozilla-central/source/mobile/android/geckoview_example).
