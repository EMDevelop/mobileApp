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

  - Open preferences > System Settings > Android SDK
  - SDK tab, you should have the latest version
  - SDK Tools tab, you should tick intel `x86 emulator acc...`

- Also, if on mac, `https://docs.expo.dev/workflow/android-studio-emulator/`
  - Need to add android SDK to path

Add the below to your `.zshrc`

```
export ANDROID_SDK=/your/path/here
export PATH=$HOME/Library/Android/sdk/platform-tools:\$PATH
```

- Then try to run `adb`

### Using Yarn workspaces

https://www.youtube.com/watch?v=um90kBJ_hG0

#### setup

- Once your Mobile app is created, you can move the contents into a `mobile` directory (do it in the finder, use `Shift + Command + >` to show hidden files)
- Put your `mobile` directory into a `packages` directory (this will be the parent)
- enter into the packages folder `cd packages`
- create a new react Application `npx create-react-app web`
- or to rename, `mv oldName/ newName`
- within packages, also create a `common` folder.
- `cd ..` to get back to the outer folder where `packages live`
- run `yarn init` and make sure `private = true`
  - Go into `packages.json`
  - add the following code to tell the app where to find our applications:

```
  "workspaces": [
    "packages/*"
  ]
```

- Make the app work with the new structure
  - Go into the `package.json` of the mobile package and add the below code.
  - This will install all the react native dependencies inside its own folder rather than in the root directory. it doesn't work well with pckages outside of the directory.

```
  "workspaces": {
    "nohoist": [
      "**"
    ]
  }
```

- Delete the node modules from mobile

```
rm -rf packages/mobile/node_modules/
rm -rf packages/mobile/yarn.lock
rm -rf packages/web/node_modules/
rm -rf packages/web/yarn.lock
```

#### I did this, it didn't tell me to, but it worked

- move the dependencies from the packages.json in the /mobile and the /web folder into the root packages.json, and add some config to run both mobile and app:

```
  "scripts": {
    "mobile": "cd packages/mobile && npm start",
    "web": "cd packages/web && npm run start"
  },
```

- run `yarn install` again in the root directory

### Using Common code

Within Common, we want to do a `yarn init`

```
cd packages/common
yarn init
change the name to @universal/common
```

Within the `mobile` and the `web` we will need to add the `common` folder as a dev dependency by adding to the packages.json

```
  "devDependencies": {
    "@universal/common": "1.0.0"
  },
```

so now we can import as... `import {something} from '@universal/common/...`
