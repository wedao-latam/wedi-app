# Overview

The Digital Wallet App serves as a demonstration of integrating social sign-in functionality with web3 wallet generation. Upon a successful user authentication, the app automatically generates a web3 wallet, linking it to the authenticated user account. Beyond this, the app supports token transaction fuctionality, allowing users to send and receive tokens, coupled with a fee estimator for customizing transaction speeds.

### Prerequisites

* Sign up for the Circle Developer account here: https://console.circle.com/signup.
* Make sure you have [Xcode](https://apps.apple.com/tw/app/xcode/id497799835?mt=12) installed for iOS app developement.
* Ensure you have [Node.js](https://nodejs.org/en/download) and [NPM](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) installed.
* Ensure you have [CocoaPods](https://formulae.brew.sh/formula/cocoapods) installed for managing iOS dependencies

### Setup Instructions
#### Frontend(iOS)
1. Navigate to the iOS App Directory
    ```bash
    cd frontend/w3s-ios-sample-app-wallets
    ```

2. Install the Dependencies
   Run the following command to install the `CircleProgrammableWalletSDK`:
    ```bash
    pod install
    ```

3. Open the App in Xcode
   Once the dependencies are installed, open the `.xcworkspace` file:
   ```bash
    open w3s-ios-sample-app-wallets.xcworkspace
    ```

4. Insert your App ID
   In Xcode, navigate to the `ContentView` file inside the `Views` folder. Replace the placeholder with your actual App ID obtained from the web3 developer console. 

5. Set Up Google Sign-In
   a. Download the `GoogleService-Info.plist`
   Navigate to the Google Developers Console, create or select a project, then enable the Google Sign-In API. Once done, you will be prompted to donwload a configuration file: `GoogleService-Info.plist`.
   b. Add `GoogleService-Info.plist` to your Xcode project.
   Ensure that the file is included in your app target.
   c. Configure URL Schemes
   Open the `Info.plist` in your Xcode project and look for the `URL Types` key. Add a new item with your reversed client ID from the `GoogleService-Info.plist`. This step ensures that after the sign-in, the app will handle the redirect back to your application correctly.

#### Backend(NextJS)
1. Navigate to the Backend Directory
    ```bash
    cd backend
    ```

2. Install the Dependencies
   Install the required packages for the backend using the following command:
    ```bash
    mpn install
    ```

3. Configure Environment Variables
   In the root of the backend directory, create a `.env` file:
   ```bash
    touch .env
    ```

    Populate the `.env` file with the following content:
    ```bash
    CIRCLE_API_KEY="YOUR_API_KEY_HERE"
    CIRCLE_BASE_URL="https://api.circle.com/v1/w3s"
    ```
    Ensure you replace `YOUR_API_KEY_HERE` with your actual API key.

## Running the App

### Frontend (iOS)

1. Run the App on a Simulator or Device
   With the `.xcworkspace` open in Xcode, select your target simulator or device, then press the play button to compile and run the app.

### Backend(NextJS)

1. Start the NextJS Server
   Initiate the backend server using:
   ```bash
    npm run dev
    ```

If you have questions, comments, or need help with code, we're here to help:

* on [Discord](https://discord.com/invite/buildoncircle)
* on Twitter at [@BuildOnCircle](https://twitter.com/BuildOnCircle)

Check out our [developer docs](https://developers.circle.com/w3s/docs).



It seems the CocoaPods version on your system is still 1.5.2. You need to update it to at least 1.13.0. Let's try updating CocoaPods again, and ensure we are using the correct installation method. Follow these steps:

### 1. Uninstall Existing CocoaPods

First, uninstall the current version of CocoaPods:

```bash
sudo gem uninstall cocoapods
```

### 2. Reinstall CocoaPods

Now, install the latest version of CocoaPods:

#### Using RubyGems:

```bash
sudo gem install cocoapods
```

#### Using Homebrew:

```bash
brew install cocoapods
```

### 3. Verify Installation

Verify that the installation was successful and that you have the correct version:

```bash
pod --version
```

You should see a version equal to or higher than 1.13.0.

### 4. Reinstall Pods

Navigate to your project directory and update the pods:

```bash
cd /path/to/your/project
pod repo update
pod install --repo-update
```

### 5. Clean Xcode Project

If the project still fails to build, try cleaning the Xcode project and deleting derived data:

```bash
rm -rf ~/Library/Developer/Xcode/DerivedData
```

Then, in Xcode, go to `Product > Clean Build Folder` (or press `Shift + Command + K`).

### Improved Podfile

Here is the updated `Podfile` with the additional necessary dependencies and enhancements:

```ruby
#  Copyright (c) 2023, Circle Technologies, LLC. All rights reserved.
#
#  Licensed under the Apache License, Version 2.0 (the "License");
#  you may not use this file except in compliance with the License.
#  You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
#  Unless required by applicable law or agreed to in writing, software
#  distributed under the License is distributed on an "AS IS" BASIS,
#  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#  See the License for the specific language governing permissions and
#  limitations under the License.

source 'https://cdn.cocoapods.org/'
source 'https://github.com/circlefin/w3s-ios-sdk.git'

platform :ios, '14.0'

target 'w3s-ios-sample-app-wallets' do
  # Use frameworks for dependencies
  use_frameworks! :linkage => :static

  # Add necessary pods
  pod 'CircleProgrammableWalletSDK'
  pod 'Firebase/Auth'
  pod 'GoogleSignIn'

  # Ensure proper Swift version
  post_install do |installer|
    installer.pods_project.targets.each do |target|
      target.build_configurations.each do |config|
        config.build_settings['BUILD_LIBRARY_FOR_DISTRIBUTION'] = 'YES'
        config.build_settings['SWIFT_VERSION'] = '5.0'
      end
    end
  end
end
```

### Summary

1. **Uninstall Existing CocoaPods**: Remove the old version.
2. **Reinstall CocoaPods**: Install the latest version.
3. **Verify Installation**: Check the CocoaPods version.
4. **Update Pods**: Run `pod repo update` and `pod install --repo-update`.
5. **Clean Xcode Project**: Remove derived data and clean the build folder.
6. **Improved Podfile**: Use the provided `Podfile` with additional dependencies and configurations.

By following these steps, you should be able to resolve the version mismatch and build errors. If you encounter any further issues, please let me know!