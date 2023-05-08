# React Native Development Environment Setup


## REQUIREMENTS

**You can only build for iOS on a Mac. So if you plan on utilizing React Native for what it's made to do, cross-platform development, you need a Mac.**

</br>

On your computer you will need to install the following. This markdown will help you to do that.

</br>

- Android Studio
- Xcode - Only on a Mac (required for iOS development)
- Watchman
- Node
- Zulu11 JDK
- Ruby - Comes pre-installed on Mac, only for iOS development
- CocoaPods - Only for iOS development

## A quick note...

You can find all of this information in the [React Native Env Setup Docs](https://reactnative.dev/docs/environment-setup). These docs offer information on installing the env for Mac, Windows or Linux. They also offer a quickstart guide for Expo. Expo is good for building very basic apps but, unfortunately, due to tha simplicity, it's not well suited to professional app development. For that reason, we are going to go with the React Native CLI setup. Additionally, due to the necessity of having a Mac for iOS development, this markdown and subsequent upcoming tutorial will be targeting Mac installation and development only. If you want to try to do this on your Windows or Linux machine, please review the docs linked above.

## Installation Directions

### Node && Watchman

All of you should already have Node since we've been using it for this entire class. But let's install [watchman](https://facebook.github.io/watchman).

```bash
brew install watchman
```

And let's double check that we have Node version 14 or higher.

```bash
node --version
```

That should output something like this `v16.15.0`.

## Ruby and Cocoapods

You should already have Ruby since you're on a Mac. But we need [cocoapods](https://cocoapods.org/). Install it by running

```bash
sudo gem install cocoapods
```

**Only do this next step if you're on a Silicon M1 or M2 Mac**

```bash
sudo arch -x86_64 gem install ffi
```

## Java Development Kit

React Native relies on a JDK or Java Development Kit to build and run correctly on the Android Platform. Let's make sure we install the recommended version.

```bash
brew tap homebrew/cask-versions
brew install --cask zulu11
```

JDK 11 is far from the newest Java version but newer versions can cause issues so we're sticking with what the docs recommend.

Now let's make sure we're using the right version by running this command...

```bash
java -version
```

You should see this.

```bash
openjdk version "11.0.14.1" 2022-02-08 LTS
OpenJDK Runtime Environment Zulu11.54+25-CA (build 11.0.14.1+1-LTS)
OpenJDK 64-Bit Server VM Zulu11.54+25-CA (build 11.0.14.1+1-LTS, mixed mode)
```

If you do, skip this next part and go straight to the Android Studio section. If you don't, follow the next steps.

## Setting default JDK to Zulu11

Get a list of your JDK versions with this command.

```bash
/usr/libexec/java_home -V
```

Copy the version number associated with Zulu11 ex. `11.0.14.1`

Run this command in your terminal.

```bash
open ~/.zprofile
```

When the text editor opens up, paste the following line of code in, making sure you add your Zulu11 version from the previous step instead of mine (11.0.14.1).

`export JAVA_HOME=$(/usr/libexec/java_home -v 11.0.14.1)`

Save that file and exit out of it. Then close your terminal and open a new window and make sure your new verison is working with the following command.

```bash
java -version
```

## Android Studio Download

Download the correct Android Studio for your Mac architecture from the links below.

- Intel Chip - [Android Studio Bumblebee for Intel](https://redirector.gvt1.com/edgedl/android/studio/install/2021.1.1.23/android-studio-2021.1.1.23-mac.dmg)
- M1 or M2 Silicon Chip - [Android Studio Bumblebee for Silicon](https://redirector.gvt1.com/edgedl/android/studio/install/2021.1.1.23/android-studio-2021.1.1.23-mac_arm.dmg)

That download is probably going to take a while. It's big. While we wait, let's get the XCode download going.

## XCode Download

Dowload XCode from the link below.

- [XCode 14](https://developer.apple.com/xcode/)

This is also going to take a while. 

## Installing the tools

Go to each of these sections once their associated download has finished.

### Android Studio Install

Run the installer with Android Studio. The defaults should be fine. Once it finishes installing, do the following steps.
 
- Open Android Studio and in the bar at the top of the screen navigate to the following `Android Studio -> Preferences`
- Once the Preferences window opens navigate in the side panel dropdowns to `Appearance & Behavior -> System Settings -> Android SDK`
- Select the `SDK Platforms` tab from within the SDK Manager, then check the box next to `Show Package Details` in the bottom right corner. Look for and expand the Android 12 (S) entry, then make sure the following items are checked:

  - Android SDK Platform 31
  - (for Intel Chips) `Intel x86 Atom_64 System Image` 
  - (for Apple M1 or M2 Silicon) `Google APIs ARM 64 v8a System Image`

- Select the `SDK Tools` tab and check the box next to `Show Package Details` here as well. Look for and expand the `Android SDK Build-Tools 33` entry, then make sure that `31.0.0` is selected.

- Finally, click `Apply` to download and install the Android SDK and related build tools.

## Final Android Studio Config

We need to configure one last thing to use Android Studio. Open your zprofile with the following command.

```bash
open ~/.zprofile
```

Paste the following lines into it and then save and close the text editor window.

```bash
export ANDROID_SDK_ROOT=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_SDK_ROOT/emulator
export PATH=$PATH:$ANDROID_SDK_ROOT/platform-tools
```

Do a hard reset of your terminal or just close it and open a new one and run the following to make sure it worked. 

```bash
echo $ANDROID_SDK_ROOT
```

You should see something like this

```bash
/Users/hunter/Library/Android/sdk
```

Then run the next check

```bash
echo $PATH
```

You should see something like this

```bash
/opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin:/Users/hunter/Library/Android/sdk/emulator:/Users/hunter/Library/Android/sdk/platform-tools
```

Congrats, once that's done, you're ready to build for Android!

### XCode Install

Install XCode from the version you downloaded. Once that's done, do the following.

- Open XCode and in the top bar go here `XCode -> Preferences`
- Once the Preferences window opens, click the `Locations` icon second from the right in the upper bar.
- Make sure the Command Line Tools: selector is on `XCode 13.3`
- Click on the `Components` icon.
- Select `iOS 14.4 Simulator` and download it

Congrats, you're now ready to build for iOS.

## Final Words

This walkthrough is set up using specific Android Studio and XCode versions because functionality can differ from version to version. If you get a role building in React Native, you will likely need to install different versions to match the ones your team is using. 