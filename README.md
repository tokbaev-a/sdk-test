# SDK Deployment Guide

## Step 1: Upload the SDK to Your GitHub Repository

1. **Download the SDK ZIP file**  

2. **Create a new repository**  
Go to your GitHub account and create a new repository for the SDK.  
Example repository name: `uptick-sdk`

3. **Extract the ZIP file**  
Unzip the previously downloaded ZIP file on your computer.

4. **Upload files to GitHub**  
Drag and drop the unzipped files into your new repository.  
Commit the changes (e.g., "Initial commit of SDK").

---

## Step 2: Update the `build.gradle` File

1. **Open the `build.gradle` file** in the `sdk` folder.

2. Look for the section that starts with:

   ```groovy
   afterEvaluate {
       publishing {
           publications {
               release(MavenPublication) {
                   from components.release
                   groupId='com.github.axeldeploy'
                   artifactId='sdk'
                   version='0.0.11'
               }
           }
       }
   }

Change the following fields:

    groupId: Replace 'com.github.axeldeploy' with your GitHub username.
    Example: 'com.github.yourusername'.
    artifactId: Keep it as 'sdk' (or rename if you prefer).
    version: Change to your desired version, like '1.0.0' for the first release.

Example after editing:

    groupId='com.github.yourusername'
    artifactId='sdk'
    version='1.0.0'
 
Save the changes and commit them to your repository.

## Step 3: Create a Release on GitHub

1. **Go to the "Releases" section of your GitHub repository.**

Find this under the "Code" tab or navigate to: https://github.com/yourusername/your-repo/releases.

2. **Click "Draft a new release".**

3. **Fill in the details:**

Tag version: Use the same version you wrote in build.gradle (e.g., 1.0.0).
Release title: Give it a title (e.g., "First Release").
Description: Add notes if you want (optional).

4. **Click "Publish release".**

## Step 4: Use JitPack to Build the SDK

1. **Go to JitPack.**

2. **Paste the link to your GitHub repository (e.g. https://github.com/yourusername/your-repo).**

3. **Click "Look Up".**

4. **Select the version (e.g., 1.0.0) you just released.**

5. **JitPack will build the SDK. If successful, it will show the dependency details you need to use the SDK.**

## Step 5: Add the SDK to Your Project Using JitPack

1. **Add JitPack to your build.gradle file:**
In your project’s root build.gradle file, add the JitPack repository at the end of the repositories section:

    ```groovy
    dependencyResolutionManagement {
        repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
        repositories {
            mavenCentral()
            maven { url 'https://jitpack.io' }
        }
    }

2. **Add the SDK dependency:**
In your module-level build.gradle (e.g., app/build.gradle), under the dependencies section, add the following:
    
    ```groovy
    dependencies {
        implementation 'com.github.yourusername:sdk:1.0.0'
    }

Replace yourusername with your GitHub username and 1.0.0 with the version you just released.

3. **Sync your project:**
After adding the dependency, sync your project with Gradle. JitPack will automatically build the SDK and make it available for use.
