---
layout: post
title: Getting Started with Windows 10 IoT Core
excerpt: "Wondering if your Pi is secretly Skynet or HAL? Stay calm and read on!"
modified: 2015-08-13
tags: [Windows 10, IoT, Pi, Windows 10 IoT Core, Windows 10 IoT Core Insider Preview, raspberry Pi 2  ]
comments: true
image:
  feature: sample-image-5.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/downloads/free-ultimate-blurred-background-pack/
---
**Updated on 26/05/2015 :** *As of the Windows 10 Pro Insider Preview Build 10122, the bug that was the source of the difficulties and frustration has been fixed!* <br /><br />So you've set up your Windows 10 IoT Core on the raspberry Pi 2 and [Hello World](http://ms-iot.github.io/content/win10/samples/HelloWorld.htm) isn't working? 

*  Getting many strange errors?
*  Currently scared, confused and wondering if your Pi is secretly Skynet or HAL?

**Stay calm and read on!**

# Step 1: Enable developer mode 

1. Search ___Settings___ in the desktop search
2. Click on ___UPDATE & SECURITY___
3. Than selcect ___For developers___ and than select ___Developer mode___

![For developers](/images/2015-05-26_17-31-15-compressor.png)

### Running a build earlier that 10122?
In earlier preview builds of Window 10 such as 10074, it was difficult and confusing to enable developer mode, as can be seen in the video below: 

<iframe width="560" height="315" src="//www.youtube.com/embed/hZmBd_EyTP8" frameborder="0" allowfullscreen="allowfullscreen">&nbsp;</iframe>

The following let you easily enable developer mode:

1.    Open an Administrator Powershell and run the following commands: 
1.    reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\AppModelUnlock" /t REG_DWORD /f /v "AllowDevelopmentWithoutDevLicense" /d "1"
1.    reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\AppModelUnlock" /t REG_DWORD /f /v "AllowAllTrustedApps" /d "1"

# Step 2: Turn on the Windows Remote Management Service

Without the Windows Remote Management Service running your Window 10 device will be unable to communicate with your Pi.

1.    Windows Key + R
1.    type services.msc
1.    Find Windows Remote Management Service.
1.    Start the service

# Step 3: Initiating a PowerShell (PS) Session

Currently an active PS session is required for visual studio to perform remote debugging on the Windows 10 IoT Core.

1.    Open an Administrator Powershell and run the following commands:
1.    Set-Item WSMan:\localhost\Client\TrustedHosts -Value <The Pi's IP Address>
1.    remove-module psreadline -force
1.    Enter-pssession -ComputerName <The Pi's IP Address> -Credential <The Pi's IP Address>\Administrator
1.    Enter p@ssw0rd in the password field 
1.    Once the shell is connected run the following command: *hostname* if the named returned is the name of the PI than your ready to go!

Please note: When replacing the <The Pi's IP Address> you must also remove the brackets.

<iframe width="560" height="315" src="//www.youtube.com/embed/gz1S-XOzmTs" frameborder="0" allowfullscreen="allowfullscreen">&nbsp;</iframe>

# Common Deployment Errors

My Pi is not outputting video to the Display?

-     If the application you're deploying has a UI, you'll need to ensure that the PI is running in headed mode by running this command: *setbootoption.exe headed* 

Feel free to tweet me comments, feedback or questions to [@ChrisBriggsy](https://twitter.com/ChrisBriggsy).