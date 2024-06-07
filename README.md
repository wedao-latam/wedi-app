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
    cd frontend/wedi-app
    ```

2. Install the Dependencies
   Run the following command to install the `CircleProgrammableWalletSDK`:
    ```bash
    pod install
    ```

3. Open the App in Xcode
   Once the dependencies are installed, open the `.xcworkspace` file:
   ```bash
    open wedi-app.xcworkspace
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



## Installation & Deployment Debugging



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

Then, in Xcode, go to `Product > Clean Build Folder` (or press `Shift + Command + K`). After cleaning the build folder, try building the project again.

### Summary

1. **Uninstall Existing CocoaPods**: Remove the old version.
2. **Reinstall CocoaPods**: Install the latest version.
3. **Verify Installation**: Check the CocoaPods version.
4. **Update Pods**: Run `pod repo update` and `pod install --repo-update`.
5. **Clean Xcode Project**: Remove derived data and clean the build folder.
6. **Improved Podfile**: Use the provided `Podfile` with additional dependencies and configurations.
7. **Open Xcode Workspace**: Open the `.xcworkspace` or `.xcodeproj` file in Xcode.
8. **Build and Run**: Try building and running the project again.



### 1. Ensure Correct Dependencies in Podfile

First, make sure your `Podfile` includes all the necessary dependencies:

```ruby
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

### 2. Update CocoaPods and Reinstall Pods

Ensure you have the latest version of CocoaPods installed and then reinstall the pods:

```bash
sudo gem install cocoapods
pod repo update
pod install --repo-update
```

### 3. Clean Xcode Project

Clean the Xcode project and delete derived data:

```bash
rm -rf ~/Library/Developer/Xcode/DerivedData
```

Then, in Xcode, go to `Product > Clean Build Folder` (or press `Shift + Command + K`).

### 4. Verify Module Import Paths

Ensure that the import statements in your Swift files match the modules provided by your dependencies. For example, the line `import Firebase` should match the module name provided by the Firebase pod.

### 5. Check for Missing or Incorrect Configuration

If the issues persist, check for any missing or incorrect configuration in your project settings:

- Go to your project settings in Xcode.
- Verify that the `Framework Search Paths` and `Header Search Paths` are correctly set up.
- Ensure that the `Build Phases` include the necessary steps to compile and link the pods.

### 6. Manual Integration (If Necessary)

If automated dependency management with CocoaPods is causing issues, you can try manually integrating the dependencies using Swift Package Manager (SPM):

- Go to `File > Swift Packages > Add Package Dependency...`
- Add the URLs for `Firebase` and `GoogleSignIn` manually.

### Debugging Specific Errors

#### No Such Module `CircleProgrammableWalletSDK`

Ensure that `CircleProgrammableWalletSDK` is correctly added to your `Podfile` and that it is available in the CocoaPods repository you are using.

#### Redefinition of Module `Firebase`

This could happen if Firebase is imported in multiple ways. Make sure you are using CocoaPods or SPM, but not both for the same module.

# Step 1: Remove .env from Git tracking but keep it locally
git rm --cached .env

# Step 2: Add .env to .gitignore to prevent future tracking
echo ".env" >> .gitignore

# Step 3: Rewrite Git history to remove .env from all commits
# WARNING: This is a destructive operation and will rewrite history!
# Make sure to backup your repository and inform all collaborators to re-clone the repository after this operation.
git filter-branch --force --index-filter \
  "git rm --cached --ignore-unmatch .env" \
  --prune-empty --tag-name-filter cat -- --all

# Step 4: Force push the changes to the remote repository
git push origin --force --all


To remove the `Pods/` directory from Git tracking history and reduce the repository size, follow these steps:

1. **Ensure `Pods/` is listed in your [`.gitignore`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2FUsers%2Fbroomva%2FGitHub%2Fwedi-app%2F.gitignore%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "/Users/broomva/GitHub/wedi-app/.gitignore") file.** It seems you've already done this.

2. **Use `git filter-branch` or a specialized tool like BFG Repo-Cleaner to remove `Pods/` from your repository's history.**

Here's how you can do it using `git filter-branch`:

```bash
# WARNING: This command will rewrite history!
# Make sure to backup your repository before running this command.
git filter-branch --force --index-filter \
  'git rm -r --cached --ignore-unmatch Pods/' \
  --prune-empty --tag-name-filter cat -- --all
```

3. **Force push the changes to your remote repository:**

```bash
git push origin --force --all
git push origin --force --tags
```

**Important Considerations:**
- **Backup your repository** before performing these operations, as they can be destructive.
- **Inform all collaborators** about the change. They will need to fetch the latest changes and may need to re-clone the repository to ensure they do not reintroduce the removed files or directories.
- For large repositories or more complex history rewrites, consider using a tool like **BFG Repo-Cleaner** for a more efficient process. BFG is faster and simpler to use for removing large files or folders from your Git history.

Here's a quick guide on using BFG Repo-Cleaner to remove the `Pods/` directory:

1. **Clone your repository using `--mirror`:**

```bash
git clone --mirror https://github.com/yourusername/yourrepository.git
```

2. **Run BFG Repo-Cleaner to remove the `Pods/` directory:**

```bash
java -jar bfg.jar --delete-folders Pods --no-blob-protection yourrepository.git
```

3. **Clean up and push the changes:**

```bash
cd yourrepository.git
git reflog expire --expire=now --all && git gc --prune=now --aggressive
git push --force
```

Remember, after performing these operations, it's crucial to run `pod install` locally to regenerate the `Pods/` directory since it won't be tracked by Git anymore.