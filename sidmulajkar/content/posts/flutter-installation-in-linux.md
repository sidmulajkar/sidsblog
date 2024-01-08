---
title: "How to install Flutter in Linux(Debian) based Systems"
categories: [flutter installation in ubuntu, linux, install flutter, flutter installation, sidsblog]
tags: [flutter, flutter installation, linux, flutter sdk, flutter docs, install flutter, ubuntu, debian, linux, android studio, sidsblog]
date: 2021-09-05T17:26:04+05:30
description: "Guide on how to install flutter in linux(debian) based system like ubuntu, popos, mint etc. Follow the steps to install flutter properly."
author: Siddhant Mulajkar
draft: false
---


![Flutter Homepage](/images/flutterimgs/flutterbn.png)

#### On Linux, you have two ways you can install Flutter.

##### Install Flutter using snapd

open your terminal and use this command to install flutter

```
sudo snap install flutter --classic
```

after installing the flutter for the first time type flutter in the terminal as it will install all its dependencies and files


```
flutter
```

wait for it to install and then move forward to the pre-requisite section.

##### Or Install FLutter Manually

If you don’t have a snapd, or can’t use it, you can install Flutter using the following steps.

1.  Download the following installation bundle to get the latest stable release of the Flutter SDK:

    [flutter_linux_2.2.3-stable.tar.xz](https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_2.2.3-stable.tar.xz)

2.  Extract the file in the desired location, for example:

```
cd ~/development
tar xf ~/Downloads/flutter_linux_2.2.3-stable.tar.xz
```

--

If you don’t want to install a fixed version of the installation bundle, you can skip steps 1 and 2. Instead, get the source code from the Flutter repo on GitHub with the following command:

```
git clone https://github.com/flutter/flutter.git
```

3.  Add the flutter tool to your path:

```
export PATH="$PATH:`pwd`/flutter/bin"
```

This command sets your PATH variable for the current terminal window only. To permanently add Flutter to your path, see Update your path.

#### How to check whether the flutter is installed properly or not?

![Flutter Version](/images/flutterimgs/flutterversionandpath.png)


---


#### Before starting the development of the first app using flutter download these pre-requisites to ensure the app works smoothly

1.  [Android Studio](https://developer.android.com/studio) / Xcode (Macos specific) 

![Android Homepage](/images/flutterimgs/androidstd.png)

#### On Linux, you have two ways to install Android Studio.

--

Either **download it directly from the site** and install it or, **use the terminal** to install it, just as you installed flutter.

```
sudo snap install android-studio --classic
```

After downloading the Android Studio open the Android Studio from the App Drawer and perform the initial setup of it.

Create an Android Emulator to test the apps developed, for this follow the images below:

![Android Studio](/images/flutterimgs/androidstudio.png)

```
Click on the More Actions and select the AVD Manager option
```

![Android AVDManager](/images/flutterimgs/avdmanager.png)


Since there will be no AVD in the starting create a new Device using the Create Virtual Device Button and leave to default options if don't want to edit the config of the device


![Android AVDCreation](/images/flutterimgs/andvirtualdeviceconfig.png)

```
Upon successful creation, the AVD should start-up
```

![Android Emulator](/images/flutterimgs/androidemulator2.png)


---

2.  **Java JDK**

To install use this command

```
sudo apt install openjdk-8-jdk
```

    Then set JAVA in path variable using

```
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
```

---

(Optional step as you can install your preferred code editor)


3.  [Visual Studio Code](https://code.visualstudio.com/) (Text editor to edit the code and install some plugins regarding the development)

![VSCODE Homepage](/images/flutterimgs/vscode.png)


Install the extensions :

1.  Flutter
2.  dart
3.  Pubsec Assist


---

#### To start and check with the Basic Hello World Project

create a directory to install the flutter app basics using the terminal

```
mkdir HelloWorld
```

```
cd HelloWorld
```

then use this command to create

```
flutter create helloworld
```

the files after the app are created using the above command

![Flutter Files](/images/flutterimgs/flutterfilesaftercreating.png)


##### Finally, time to run the flutter app

```
flutter run
```

![Flutter App](/images/flutterimgs/androidemulatorapprun.png)


---


##### If you still face the issue then use the flutter doctor command to find out what's not installed and needs a look

```
flutter doctor
```

---


#### Hope this tutorial helped you in some way. Thank you for following it.

---

### Read More Blogs related to:

***[db-concepts]({{< relref "/tags/database/">}}) / [linux]({{< relref "/tags/linux">}}) / [flutter-installation]({{< relref "/tags/flutter">}}) / [networking]({{< relref "/tags/networking">}}) / [raspberry-pi]({{< relref "/tags/raspberry">}})***

--