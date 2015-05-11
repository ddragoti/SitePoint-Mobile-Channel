# Top 8 plug-ins for Android Studio
[Android Studio](http://developer.android.com/tools/studio/index.html) is now the official Google IDE designed for native Android application development. Based on JetBrains' [IntelliJ IDEA](https://www.jetbrains.com/idea/), it was first announced at Google I/O 2013 as the successor to Eclipse and was generally welcomed by the Android community. After a long beta phase, the final version was announced in December of last year.

Android Studio is a fully-featured development environment equipped with everything needed to develop Android applications for all devices, from smart watches to automobiles. There is always room for improvement and Android Studio offers support for third party plug-ins, and this article will list some of the most useful.

## 1. H.A.X.M (Hardware Accelerated Execution Manager)
H.A.X.M is the best way for developers who use the Android Emulator to execute their applications faster. H.A.X.M provides hardware acceleration for Android SDK emulators on Intel systems. It uses Intel Virtualization Technology (Intel VT) built on top of virtualization hardware VT-X. This means processors that support virtualization, giving the fastest way to run applications on simulated Android environments. I think that H.A.X.M is the most useful plugin that an Android developer can have to run the latest Android version on the emulator as fast as possible.

### To install H.A.X.M
Open the Android SDK Manager, select the "Intel x86 Emulator Accelerator (HAXM installer)", accept the license and install the package.

![](https://github.com/valdio/SitePoint-Mobile-Channel/blob/master/Articles/Valdio%20Veliu/10%20Plugins%20For%20Android%20Studio/images/haxm.PNG)

This process has downloaded the package but not installed H.A.X.M. To finish the installation go to the SDK path shown in the image above `C:\Users\Administrator\AppData\Local\Android\sdk\` (This installation is on a Windows machine) and try to find the download folder. Mine was `C:\Users\Administrator\AppData\Local\Android\sdk\extras\intel`. Open the installation folder `Hardware_Accelerated_Execution_Manager`, click the executable `intelhaxm-android` and continue the installation. After this installation you are ready to use the emulator.

![](https://github.com/valdio/SitePoint-Mobile-Channel/blob/master/Articles/Valdio%20Veliu/10%20Plugins%20For%20Android%20Studio/images/haxmexe.PNG)

## 2. Genymotion
![](https://raw.githubusercontent.com/valdio/SitePoint-Mobile-Channel/master/Articles/Valdio%20Veliu/10%20Plugins%20For%20Android%20Studio/images/0.PNG)

Genymotion is the ultimate tool for testing your Android application and enables you to run custom versions of Android. It's built for execution inside VirtualBox and equipped with the complete set of sensors and features needed to interact with a virtual Android environment. With Genymotion, you can test your Android applications on a wide range of virtual devices for development and its emulators are a lot faster than the default emulator.

Every developer who wants to make sure their application runs smoothly on every supported device and has trouble troubleshooting specific device errors should make use of this great plugin.

To install Genymotion follow [our previous tutorial](http://www.sitepoint.com/improved-android-emulation-genymotion/) .

## 3. Android Drawable Importer
![](https://github.com/valdio/SitePoint-Mobile-Channel/blob/master/Articles/Valdio%20Veliu/10%20Plugins%20For%20Android%20Studio/images/drawable1.PNG)

![](https://github.com/valdio/SitePoint-Mobile-Channel/blob/master/Articles/Valdio%20Veliu/10%20Plugins%20For%20Android%20Studio/images/drawable2.PNG)

To adapt to all Android screen sizes and densities, each Android project contains the _drawable_ folder. Any developer with experience of Android development knows that to support all the screen sizes you must import different drawables for each screen type. The Android Drawable Importer makes this job easier. It reduces the effort needed to import scaled images into the Android project. Android Drawable Importer adds an option to import drawables in different resolutions or scale a specified image to a defined resolution. This plugin speeds up every developer's work with drawables.

### To install Drawable Importer:
![](https://github.com/valdio/SitePoint-Mobile-Channel/blob/master/Articles/Valdio%20Veliu/10%20Plugins%20For%20Android%20Studio/images/Drawable%20Importer.gif)

## 4. Android ButterKnife Zelezny
Android ButterKnife is a "View Injection Library for Android". It gives a better view of code and makes it more readable. ButterKnife allows you to focus on the logic rather than glue code for finding views or adding listeners. Programing with ButterKnife you have to perform injection on arbitrary objects, they take this form:

```
 @InjectView(R.id.title) TextView title;
```

If you have one or two injections, writing them is not a problem, but if you have more, you need to refer to all the layout XMLs to write them in the source file.

Android ButterKnife Zelezny is a Android Studio Plugin for generating ButterKnife injections from selected layout XMLs in activities, fragments or adapters. The plugin will provide the fastest way to generate your XML object injections.

Here is an example of how code looks before using Android ButterKnife:

![](https://github.com/valdio/SitePoint-Mobile-Channel/blob/master/Articles/Valdio Veliu/10 Plugins For Android Studio/images/bk1.PNG)

And after:

![](https://github.com/valdio/SitePoint-Mobile-Channel/blob/master/Articles/Valdio%20Veliu/10%20Plugins%20For%20Android%20Studio/images/bk2.PNG)

### To install ButterKnife Zelezny:
![](https://github.com/valdio/SitePoint-Mobile-Channel/blob/master/Articles/Valdio%20Veliu/10%20Plugins%20For%20Android%20Studio/images/ButterKnife%20Zelezny.gif)

## 5.Android Holo Colors Generator
To develop Android applications you should need a great design and layout. The Android Holo Colors Generator is the easiest way to customize your Android application, matching your own preferences. Android Holo Colors Generator is a plugin that allows you to create Android layout components from your own colors for your application. This plugin will generate all the necessary assets associated with XML drawables and styles to use in your project.

### To install Holo Colors Generator:
![](https://github.com/valdio/SitePoint-Mobile-Channel/blob/master/Articles/Valdio%20Veliu/10%20Plugins%20For%20Android%20Studio/images/Holo%20Colors%20Generator.gif)

## 6. Robotium Recorder
Robotium Recorder is a test automation framework for testing native and hybrid mobile applications on emulators and Android devices. With Robotium Recorder it's possible to record test cases and user actions. You can view functions of system and user test scenarios on different Android activities.

With Robotium Recorder you can see what's happening with your application when it runs on your device, if it's working as expected or if it reacts properly to user actions. For everyone who is looking to develop stable Android applications this plugin is helpful for thorough testing.

Here is an example of my application recorded on Robotium Recorder:

![](https://github.com/valdio/SitePoint-Mobile-Channel/blob/master/Articles/Valdio%20Veliu/10%20Plugins%20For%20Android%20Studio/images/Robotium.jpg)

To install Robotium Recorder visit the [official page](http://robotium.com) and in the Installation section choose the version of Robotium Recorder based on your Operating System.

## 7. jimu Mirror
Android Studio is equipped with a visual layout editor, but a static preview of the layout might not be enough. With a static preview it is not possible to preview animation, colors and touch zones, so jimu Mirror is a plugin that allows you to test your layout on the fly on a real device. Jimu Mirror gives you on-device previews of Android layouts that update as you code. This plugin offers a realistic context before you start coding.

### To install jimu Mirror:
![](https://github.com/valdio/SitePoint-Mobile-Channel/blob/master/Articles/Valdio%20Veliu/10%20Plugins%20For%20Android%20Studio/images/jimu%20Mirror.gif)

## 8. strings-xml-tools
Strings-xml-tools is a small but useful plugin that can be used to manage the string resources in Android projects. It provides basic operations for sorting entries in Android localization files and adding missing strings. The plugin is limited but if your application has a large number of string resources this plugin might be helpful.

### To install Android Strings.xml tools:
![](https://github.com/valdio/SitePoint-Mobile-Channel/blob/master/Articles/Valdio%20Veliu/10%20Plugins%20For%20Android%20Studio/images/Android%20Strings.xml%20tools.gif)
