# MobileApp

This is a mobile app, built from scratch with the help of Mosh https://www.youtube.com/watch?v=0-S5a0eXPoc. It is built using Expo CLI for a fast mobile app production.

## Tutorial Notes

### CLI Framework options.

Expo CLI

- This is a simpler framework with a higher level of abstraction, allowing you to build fast mobile apps. Only Javascript code, no reference to IOS and Android.

React Native CLI

- Useful for those who have IOS and Android previous experience, will have two directories (one for each of those).

### Install

```
sudo npm i -g expo-cli
```

Install the following:

- `expo client` app on your phone (it is an emulator, cross platform)
- `React Native Tools` on VScode
- `React-Native/React/Redux snippets for es6/es7` on vs code

### Create App

```
expo init AppName
```

Then choose between workflows:

- Managed: We won't see the IOS and Android directories
- Bare: We will see the IOS and Android projects, this will be a react native project

For this though, we're choosing the `Managed workflow` option:

```
blank         a minimal app as clean as an empty canvas
```

### General

- In react native, there are no traditional div, txt components. We havr to use imported components from `react-native`

### File Structure

`assets`

- This is where we put Images, Audio files, Images

`App.js`

- This comes with some boiler plate code
  - Imports
    - `View`
      - this is basically a `div` in the rect works
      - Mapped to `UIview` or `Android view` when compiled.
    - `Text`
      - this is used to display text on screen
    - `Stylesheet`
      - This is how we create style, there is no CSS.

### Start

```
cd TestApp
npm start
```

- This will open `metro bundler` on `localhost:19002`
- Also, in the terminal you get an option to run in IOS, Android bla

### Emulator

##### IOS

- Download Xcode in the Apple Appstore
- When downloaded, Go to `Preferences>Locations` and make sure you have the latest command line tools.
- Now you can either open the app in the simulator using `metro bundler` or typing `i` in the terminal.
- The changes are changed using `hot reload` (actually it is called `fast refresh`) when we change anything in the code.
- Inside the simulator, press `ctrl + d` and then `command + d` will open the developer menu

##### Android

- Download Android Studios `https://developer.android.com/studio`

  -

- Also, if on mac, `https://docs.expo.dev/workflow/android-studio-emulator/`
  - Need to add android SDK to path

```
[ -d "$HOME/Library/Android/sdk" ] && ANDROID_SDK=$HOME/Library/Android/sdk || ANDROID_SDK=$HOME/Android/Sdk
echo "export ANDROID_SDK=$ANDROID_SDK" >> ~/`[[ $SHELL == *"zsh" ]] && echo '.zshenv' || echo '.bash_profile'`

echo "export PATH=$HOME/Library/Android/sdk/platform-tools:\$PATH" >> ~/`[[ $SHELL == *"zsh" ]] && echo '.zshenv' || echo '.bash_profile'`

```

- Then try to run `adb`
