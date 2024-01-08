---
title: "Step-by-Step Guide: Installing Ubuntu with Linux Subsystem WSL-2 on Windows 10 for Hassle-free Setup"
categories: [how to install wsl in windows, wsl, wsl2, wsl 2, wsl2 install, wsl install, docker wsl2, docker desktop, windows wsl, windows subsystem for linux, linux, windows10, ubuntu installation, guide, sidsblog]
tags: [how to install wsl in windows, wsl, wsl2, wsl 2, wsl2 install, wsl install, docker wsl2, docker desktop, windows wsl, windows subsystem for linux, linux, windows10, ubuntu installation, guide, sidsblog]
date: 2021-09-23T17:26:04+05:30
description: "Best tutorial on how to install ubuntu using linux subsystem wsl2 on windows 10"
author: Siddhant Mulajkar
draft: false
---

**So, Ready to transform your Windows Environment in to your Linux Beast!!**

![WSL Arch Image](/images/windowswsl2/wslarch.png)


---


###### Before prcoeeding with the tutorial check if you have the proper version of Windows 10 installed using the winver command in Windows Start options or using the "Run" command to use the WSL-2.

![Winver Image](/images/windowswsl2/winverwindows.jpg)

###### If you don't have the similar version then try the updating the windows to work ahead.

##### 1.    Once you have the windows proper version then again open the windows start menu and then type "Turn on or off Windows Features" to open the dialog box as shown below.

![Windows Feature](/images/windowswsl2/windowsfeatures.png)

1.1.    Then check the following options and uncheck others which are not required. 

![Windows Feature1](/images/windowswsl2/windowsfeatures1.png)  

1.2.    Restart the Computer for the changes to take effect

##### 2.    Once you restart open the microsoft store and download the new and recent Windows Terminal and the Ubuntu accordingly.

![Windows Terminal](/images/windowswsl2/windowsterminal1.png) 

![Windows Terminal](/images/windowswsl2/windowsterminal.png)


![Windows Terminal](/images/windowswsl2/windowster2.jpeg)

##### What is Windows Terminal?

Windows Terminal is a modern terminal application for users of command-line tools and shells like Command Prompt, PowerShell, and Windows Subsystem for Linux (WSL). Its main features include multiple tabs, panes, Unicode and UTF-8 character support, a GPU accelerated text rendering engine, and the ability to create your own themes and customize text, colors, backgrounds, and shortcuts.

---

2.1.    Similarly, install the ubuntu image from the Store itself. It is around 500mb might a few minutes to download the system depending upon the internet connectivity.

![Install Ubuntu Store](/images/windowswsl2/ubuntudownload1.png)

---

2.2.    After downloading it, before running and installing it download a another linux kernel update package given in the link.

https://docs.microsoft.com/en-us/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package

![Install Ubuntu Store](/images/windowswsl2/ifubuntugiveserrordownloadswsl.png)

---

2.3.    After the installation process, open the ubuntu from the windows start menu and let it install.

![First boot of Ubuntu](/images/windowswsl2/ubuntufirstboot.png)

---

2.4.    Open the windows terminal that you downloaded and type the command

```
wsl -l -v
```

![Check the Linux Running](/images/windowswsl2/ifeverythingbootsproperly.png)

2.5.    It works!! But we need to upgrade the linux subsystem from running in wsl1 to wsl2 for better linux subsystem handling and features. To do that use the command

```
wsl --shutdown
```

```
wsl --list --verbose
```

```
wsl --set-version Ubuntu-20.04 2
```

![Wsl Update](/images/windowswsl2/wsl1towsl2upgrade.png)

The conversion will never delete the files of the Linux Subsystem if you ever want to convert it and might take 2-3 minutes for completing the process.

### That's it, the linux subsystem is good to use!! You have successfully installed ubuntu on Windows. Just update and upgrade the linux before installing any packages.

```
{
    sudo apt update 

    sudo apt upgrade
}
```
---

##### 3.    If you don't want to use the different terminal of windows and ubuntu and want to start the ubuntu when you load the Windows terminal itself then follow along ...

3.1.    Open the windows terminal and go to the settings by clicking the arrow down key from the new tab sign and select settings from the menu.

![Wsl Update](/images/windowswsl2/newterminalsettings.png)

---

3.2.    There are two ways, either select the option from the dropdown menu after "Default profile" name or click the last option in the left sidebar "Open JSON file"

![Settings Options](/images/windowswsl2/needtochangewithubuntu1.png)

##### or

Just change the default guid no with the ubuntu subsystem guid
 
![Settings Options](/images/windowswsl2/needtochangewithubuntu.png)

##### Again save and close the settings section and the terminal and open, as you might see, it now opens the Ubuntu Directly rather than the terminal.

![Ubuntu Set to Default](/images/windowswsl2/oncechangewithubuntu1.png)

---

##### 4.    Set your WSL distribution to start in the home ~ directory when launched

By default, the startingDirectory of a profile is %USERPROFILE% (C:\Users\<YourUsername>). This is a Windows path. For WSL, however, you may want to use the WSL home path instead. startingDirectory only accepts a Windows-style path, so setting it to start within a WSL distribution requires a prefix.

Beginning in Windows 10 version 1903, the file systems of WSL distributions can be addressed using the \\wsl$\ prefix. For any WSL distribution with the name DistroName, use \\wsl$\DistroName as a Windows path that points to the root of that distribution's file system.

For example, the following setting will launch the "Ubuntu-18.04" distribution in its home file path:

```
{
    "name": "Ubuntu-18.04",
    "commandline" : "wsl -d Ubuntu-18.04",
    "startingDirectory" : "//wsl$/Ubuntu-18.04/home/<Your Ubuntu Username>"
}
```

![Wsl Home Directory](/images/windowswsl2/wslhomedir.png)


![Wsl Home Directory](/images/windowswsl2/wslhomedir1.png)

---


###### 5.   How to open WSL Home Directory in the Windows Explorer for better file management

Go to the home directory of the wsl and use this command to load the explorer using it

```
explorer.exe .
```

![File Explorer WSL](/images/windowswsl2/explorer.png)

![File Explorer WSL](/images/windowswsl2/explorer1.png)


**Additional Guide/Troubleshooting Link:**

https://docs.microsoft.com/en-us/windows/terminal/troubleshooting#:~:text=the%20Actions%20page.-,Set%20your%20WSL%20distribution%20to%20start%20in%20the%20home%20~%20directory,the%20WSL%20home%20path%20instead


---

**And that’s it! WSL-2 with the new Linux Setup is set for better development process using various tools.**

---

### Read More Blogs related to:

***[db-concepts]({{< relref "/tags/database/">}}) / [linux]({{< relref "/tags/linux">}}) / [flutter-installation]({{< relref "/tags/flutter">}}) / [networking]({{< relref "/tags/networking">}}) / [raspberry-pi]({{< relref "/tags/raspberry">}})***

--