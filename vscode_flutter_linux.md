### Linux下使用vscode开发Flutter环境配置相关问题


#### 安装Flutter:

> [Get Started: Install on Linux](https://flutter.io/setup-linux/)

#### Add Flutte bin to PATH:

> Edit $HOME/.profile, add

> `PATH="$PATH:$HOME/devprojects/flutterdev/flutter/bin"` as the last line of the file.


#### Ubuntu下安装Android Studio的问题:

> According to:[Android Studio Install Step Linux.4](https://developer.android.com/studio/install)

中文版本的文档是有错误的.选择English就可以看到:

    If you are running a 64-bit version of Ubuntu, you need to install some 32-bit libraries with the following command:
    
> `sudo apt-get install libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1 libbz2-1.0:i386`
    
#### Start Android Studio and check for update:

> To launch Android Studio, open a terminal, navigate to the android-studio/bin/ directory, and execute `. ./studio.sh`

> On the Android Studio startup screen, use Configure->Check For Updates to check for AS updates.


#### Run flutter doctor

> Run the following command to see if there are any dependencies you need to install to complete the setup:

> `flutter doctor`

#### Set up your Android device

> To prepare to run and test your Flutter app on an Android device, you’ll need an Android device running Android 4.1 (API level 16) or higher.

> Enable Developer options and USB debugging on your device. Detailed instructions are available in the Android documentation.
Using a USB cable, plug your phone into your computer. If prompted on your device, authorize your computer to access your device.
In the terminal, run the:

> `flutter devices` 

>command to verify that Flutter recognizes your connected Android device.
Start your app by running flutter run.
By default, Flutter uses the version of the Android SDK where your adb tool is based. If you want Flutter to use a different installation of the Android SDK, you must set the ANDROID_HOME environment variable to that installation directory.

![flutter devices命令](imgs/flutter_devices.png)

