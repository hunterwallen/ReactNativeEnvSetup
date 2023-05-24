# React Native Development Environment Setup
*Last Updated: May 24th, 2023*


## REQUIREMENTS


## Something to note...

**_You can only build for iOS on a Mac. So if you plan on utilizing React Native for what it's made to do, cross-platform development, you need a Mac._**

Due to the necessity of having a Mac for iOS development, this markdown and subsequent upcoming tutorial will be targeting Mac installation and development only. If you want to try to do this on your Windows or Linux machine, please review the docs linked above. Just be aware that you cannot install XCode on a Linux or Windows machine and you MUST have Xcode to be able to run iOS emulators or build for iOS. Since the Javascript/Typescript code you write the bulk of React Native in will run on BOTH Android and iOS, you can still develop on Windows and Linux. However, since the biggest benefit of using React Native is it's ability to build for both Android and iOS devices, you will inevitably want to test your app and then build it to submit to the Apple App Store on a Mac. Additionally, you will almost certainly run into small bugs, styling issues and other roadblocks when you eventually run you app on a Mac to test and build for iOS so professional React Native developers always use a Mac.


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

## Expo vs React Native CLI

You can find all of this information in the [React Native Env Setup Docs](https://reactnative.dev/docs/environment-setup). These docs offer information on installing the env for Mac, Windows or Linux. They also offer a quickstart guide for Expo. Expo is good for building very basic apps but, unfortunately, due to the simplicity, it's not well suited to professional app development. Expo abstracts away the native code in the ```android``` and ```ios``` folders, making it impossible to use React Native libraries that require native integration (think using the gps, accelerometer, push notifications etc). Instead you're forced to use libraries from a much smaller, Expo-specific ecosystem which severely limits your options for many pieces of functionality essential for mobile development. For that reason, we are going to go with the React Native CLI setup. This approach makes things a little more complicated to learn at first but will ensure that your skills are robust enough to use React Native professionally.

In the future, if you are using the docs to set up your development environment, make sure you have selected React Native CLI and your operating system to ensure you aren't installing the wrong dependencies.

## Installation Directions

## Update Homebrew
To ensure we're installing the most up to date versions of these packages, let's preemtively update homebrew.

Run the follwing command in your terminal
```bash
brew update
```

## Node & Watchman

All of you should already have Node since we've been using it for this entire class. But let's install [watchman](https://facebook.github.io/watchman).

```bash
brew install watchman
```

And let's double check that we have Node version 14 or higher.

```bash
node --version
```

That should output something like this `v16.15.0`. If your version isn't an exact match, that's okay. Just make sure you're not on a lower version than 14.

## Ruby & Cocoapods

You should already have Ruby since you're on a Mac but unfortunately you will need to use a different version for React Native. Since some of the other things on your machine may need the version that comes preinstalled, we're going to install a Ruby Version Manager called `rbenv` that's similar to `pyenv` for Python. Additionally, if you are on an M1 or M2 Mac, we will need to install a package called `ffi` in order to make sure our ruby env is compatible with legacy packages published before the silicon chips came out.


1. Use brew to install rbenv and ruby-build
```bash
brew install rbenv ruby-build
```

2. Install the correct Ruby version using rbenv
```bash
rbenv install 2.7.6
```

3. Set that Ruby version globally
```bash
rbenv global 2.7.6
```

4. Export the rbenv global config vars and rbenv init command to your .zshrc file to make it run every time a new terminal instance opens
```bash
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc && echo 'eval "$(rbenv init -)"' >> ~/.zshrc
```

5. Close/kill your terminal and open a new one

6. Check to make sure you have the correct Ruby version running
```bash
ruby -v
```
You should see something like `2.7.6`. If you do, move to step 7 if you are on an M1 or M2 or skip step 8 if you're on an Intel. 

**_If you don't see the correct version follow these troubleshooting instructions:_**

Open up your .zshrc file with 
```bash
open ~/.zshrc
```
and make sure you see the following lines:
```
export PATH="$HOME/.rbenv/bin:$PATH"
eval "$(rbenv init -)"
```
Also make sure you have completely closed your terminal and opened a new one. Finally, if that still doesn't show the correct version, rerun steps 1 -4, making sure none of those steps ended with an error.

**IMPORTANT!!!** *ONLY DO STEP 7 IF YOU'RE ON A SILICON M1 OR M2 MAC*

7. Install the Ruby gem ffi to allow the silicon chip to work with legacy Ruby libraries
```bash
sudo arch -x86_64 gem install ffi
```

**Once you've completed the previous section...**

Now that we have the right ruby version, we will also need [cocoapods](https://cocoapods.org/). Install it by running

```bash
sudo gem install cocoapods
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

Run this command in your terminal to set your Zulu11 version as your default Java version.
```bash
echo 'export JAVA_HOME=$(/usr/libexec/java_home -v 11.0.14.1)' >> ~/.zshrc
```

Close/kill your terminal and open a new terminal instance and make sure your new verison is set with the following command.

```bash
java -version
```

You should see the version you included in the following command. If you do, move on to the Android Studio download section. If you don't open up and check your .zshrc file to make sure you have the following line in it:

```
export JAVA_HOME=$(/usr/libexec/java_home -v 11.0.14.1)
```

If you do, try to completely kill your terminal and open a new window and check the version again. If that doesn't work, double check that your installation was successful by rerunning the brew install zulu11 command above. You won't need to run the echo command with the Java version in it if that line is already in your .zshrc file.

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

  - Android API 33 -> Android SDK Platform 33, Sources for Android 33, Sources for Android 33
  - Google API's box associated with you platform:
    - (for Intel Chips) `Google APIs Intel x86_64 Atom System Image` 
    - (for Apple M1 or M2 Silicon) `Google APIs ARM 64 v8a System Image`

- Select the `SDK Tools` tab at the top center of that same Android SDK section and check the box next to `Show Package Details` here as well. Look for and expand the `Android SDK Build-Tools 34rc4` entry, then make sure that `33.0.0` is selected.

- Finally, click `Apply` to download and install the Android SDK and related build tools.


## Create your first emulator
This first time you use Android Studio, you have to create an emulator so that your apps have an Android device on your machine they can run on. You only have to do this once if you only want to use a single emulator. Since different phones have different screen sizes and aspect ratios, you can and should create many different devices for testing purposes in the future but for our purposes for our Intro Lesson, we're just going to use one.

- After you close the Preferences Windown and on the home screen for android studio, click the three vertical dots next to the Get From VCS button in the top right hand section of the window and select `Virtual Device Manager`

- Click `Create New Device` in the top left of the window that opened. 

- Select a Pixel 4 XL and then click `Next`

- Select API 33 and click `Next`

- Click `Finish` to create the emulator so that when we run our app from the CLI on Android, there will be an emulator for it to run on.

## Final Android Studio Config

We need to configure one last thing to use Android Studio and that is to configure your terminal to contain the paths to the android sdk root and extension paths.

1. Run the following commands in your terminal:
```bash
echo 'export ANDROID_SDK_ROOT=$HOME/Library/Android/sdk' >> ~/.zshrc && echo 'export PATH=$PATH:$ANDROID_SDK_ROOT/emulator' >> ~/.zshrc && echo 'export PATH=$PATH:$ANDROID_SDK_ROOT/platform-tools' >> ~/.zshrc
```

2. Close/kill your current terminal and open a new one and run the following to make sure it worked. 

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

Congrats, once that's done, you're ready to build and run React Native apps for Android!

### XCode Install

Install XCode from the version you downloaded. Once that's done, do the following.

- Open XCode and in the top bar go here `XCode -> Preferences`
- Once the Preferences window opens, click the `Locations` icon second from the right in the upper bar.
- Even if it's already selected, click on the Command Line Tools: selector and select `XCode 14.0` or whatever version you have installed. It's very important that you actually open the selector and choose it. Just because it appears selected doesn't mean it is. It's a bug in Xcode that is super annoying but easy to avoid. 
- Click on the `Platforms` icon.
- Select the `GET` button associated with the `iOS 15.2 Simulator` and download it. If you see a different version, that's fine, just make sure you click get to download the iOS Simulator associated with your Xcode version.

Congrats, you're now ready to build and run React Native apps for iOS.

## Final Thing to Keep In Mind

This walkthrough is set up using specific Android Studio and XCode versions available at the time it was created. Unfortunately, there is often variations across different versions of Xcode and Android Studio as well as shifting requirements in each new React Native release. If you are using this markdown and there is some piece that isn't up to date, you may need to do a little GoogleFu to find out how to accomplish what's needed for that step. Once you do, congratulate yourself because you just got a taste of what mobile cross-platform development entails. There is a reason mobile engineers are paid more than web developers and it's because it is a rapidly evolving and ever-shifting ecosystem with far more moving parts and far less consistency than browser based development. If you get a role building in React Native, you will likely need to be able to navigate and troubleshoot a variety of sitations evolving out of a change in UI, functionality or compatibility across different Xcode, Android Studio, Android, iOS, React Native and third-party library versions. The good news is, React Native is a very well-supported and widely used open-source platform and you can almost always find good solutions to issues you run into by reading the most recent React Native docs and leveraging Stack Overflow. So flex those independence muscles and practice helping yourself if you run into issues and it will serve you well should you choose to pursue this technology professionally.