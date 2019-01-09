# Debugging Native Code in Android Studio.
If you want to work on the C++ code that powers GeckoView, you will need to be able to perform native debugging inside Android Studio. This article will guide you through how to do that. 

If you need to get set up with GeckoView for the first time, follow the [Quick Start Guide](GeckoViewQuickStart.md).

## Perform a debug build of Gecko.
1. Edit your `mozconfig` file and add the following lines. These will ensure that the build is performed generating debug symbols.

```
ac_add_options --enable-debug
ac_add_options --enable-debug-symbols
ac_add_options --with-android-ndk="<path>/.mozbuild/android-ndk-r17b"
```
2. Ensure that the following lines are commented out in your `mozconfig` if present. `./mach configure` will not allow artifact builds to be enabled when generating a debug build.

```
# ac_add_options --enable-artifact-builds
```
3. To be absolutely sure that Android Studio will pick up your debug symbols, the first time you perform a debug build it is best to clobber your `MOZ_OBJDIR`. Subsequent builds should not need this step.

```bash
./mach clobber
```
4. Build as usual. Because this is a debug build, and because you have clobbered your `MOZ_OBJDIR`, this will take a long time. Subsequent builds will be incremental and take less time, so go make yourself a cup of your favourite beverage. 
Once the build is complete, don't forget to package, otherwise Android Studio will not pick up your changes and symbols.

```bash
./mach build
./mach package.
```
## Set up lldb to find your symbols
Edit your `~/.lldbinit` file (or create one if one does not already exist) and add the following lines. 

The first line tells LLDB to enable inline breakpoints - Android Studio will need this if you want to use visual breakpoints. 

The remaining lines tell LLDB where to go to find the symbols for debugging.

```bash
settings set target.inline-breakpoint-strategy always
settings append target.exec-search-paths <PATH>/objdir-android-opt/toolkit/library
settings append target.exec-search-paths <PATH>/objdir-android-opt/mozglue/build
```
# Set up Android Studio to perform native debugging.

1. Edit the configuration that you want to debug by clicking `Run -> Edit Configurations...` and selecting the correct configuration from the options on the left hand side of the resulting window.
2. Select the `Debugger` tab.
3. Select `Native` or `Dual` from the `Debug type` select box. Native will only allow for debugging native code, whereas Dual will allow debugging of both native and Java code in the same session.
4. Under `Symbol Directories`, add a new path pointing to `<PATH>/objdir-android-opt/toolkit/library`, the same path that you entered into your `.lldbinit` file.
5. Select `Apply` and `OK` to close the window.

# Debug Native code in Android Studio

1. The first time you are running a debug session for your app, it's best to start from a completely clean build. Click `Build -> Rebuild Project` to clean and rebuild. You can also choose to remove any existing builds from your emulator to be completely sure, but this may not be neccessary.
2. If using Android Studio visual breakpoints, set your breakpoints in your native code. 
3. Run the app in debug mode as usual.
4. When debugging Fennec or geckoview_example, you will almost immediately hit a breakpoint in `ElfLoader.cpp`. This is expected. If you are not using Android Studio visual breakpoints, you can set your breakpoints here using the lldb console that is available now this breakpoint has been hit. To set a breakpoint, select the app tab (if running Dual, there will also be an `<app> java` tab) from the debug window, and then select the `lldb` console tab. Type the following into the console:

```lldb
b <file>.cpp:<line number>
```
5. Once your breakpoints have been set, click the continue execution button to move beyond the `ElfLoader` breakpoint and your newly set native breakpoints should be hit. Debug as usual.