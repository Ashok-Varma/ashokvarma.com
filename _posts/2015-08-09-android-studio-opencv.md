---
title: "Integrate Android Studio with OpenCV"
layout: post

categories: post
tags:
---

You can do this very easily in Android Studio.

## Follow the below steps to add Open CV in your project as library.

1.  Create a `libraries` folder underneath your project main directory. For example, if your project is`OpenCVExamples`, you would create a `OpenCVExamples/libraries` folder.
2.  Go to the location where you have SDK “\\OpenCV-2.4.8-android-sdk\\sdk” here you will find the `java` folder, rename it to `opencv`.
3.  Now copy the complete opencv directory from the SDK into the libraries folder you just created.
4.  Now create a `build.gradle` file in the `opencv` directory with the following contents

    ```gradle
    apply plugin: 'android-library'

    buildscript {
        repositories {
            mavenCentral()
        }
        dependencies {
            classpath 'com.android.tools.build:gradle:0.9.+'
        }
    }

    android {
        compileSdkVersion 19
        buildToolsVersion "19.0.1"

        defaultConfig {
            minSdkVersion 8
            targetSdkVersion 19
            versionCode 2480
            versionName "2.4.8"
        }

        sourceSets {
            main {
                manifest.srcFile 'AndroidManifest.xml'
                java.srcDirs = ['src']
                resources.srcDirs = ['src']
                res.srcDirs = ['res']
                aidl.srcDirs = ['src']
            }
        }
    }
    ```

5.  Edit your settings.gradle file in your application’s main directory and add this line:

    ```gradle
    include ':libraries:opencv'
    ```

6.  Sync your project with Gradle and it should looks like this.![Module Settings](http://i1.wp.com/ashokvarma.me/wp-content/uploads/2015/08/8Dcx9.png?resize=640%2C351)
7.  Right click on your project then click on the `Open Module Settings` then Choose Modules from the left-hand list, click on your application’s module, click on the Dependencies tab, and click on the + button to add a new module dependency.
    ![Dependency Addition](http://i1.wp.com/ashokvarma.me/wp-content/uploads/2015/08/A34Dx.png?resize=640%2C326)
8.  Choose `Module dependency`. It will open a dialog with a list of modules to choose from; select “:libraries:opencv”.
    ![Module Dependency](http://i1.wp.com/ashokvarma.me/wp-content/uploads/2015/08/EnZNx.png?resize=640%2C380)
9.  Create a `jniLibs` folder in the `/app/src/main/` location and copy the all the folder with \*.so files (armeabi, armeabi-v7a, mips, x86) in the `jniLibs` from the OpenCV SDK.
    ![JniLibs](http://i1.wp.com/ashokvarma.me/wp-content/uploads/2015/08/ufun9.png?resize=640%2C260)
10.  Click OK. Now everything done, go and enjoy with OpenCV.

## OpenCV Initialisation :

add this static block to activity in which you are using OpenCV functions.

```java
static {
  if (!OpenCVLoader.initDebug()) {
  // Handle initialization error
  }
}
```
