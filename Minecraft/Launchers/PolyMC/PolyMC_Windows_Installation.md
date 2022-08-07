# Installing PolyMC on Windows and more!

# Preface
What is PolyMC? - PolyMC is a fork of the popular Minecraft launcher, MultiMC.

# Installing Java 8 & 18
We will be getting Java from `adoptium.net`. Navigate to <https://adoptium.net/temurin/releases>.

## Downloading the Java installers
For both Java 8 and Java 18, select the following:
* `Operating System`: Windows
* `Architecture`: x64
* `Package Type`: JRE

For Java 8, also select the following:
* `Version`: 8
<br> then scroll a bit down and click ![](./PolyMC_Windows_Installation/java_installers_msi_download_button.png) to download.

For Java 18, also select the following:
* `Version`: 18
<br> then scroll a bit down and click ![](./PolyMC_Windows_Installation/java_installers_msi_download_button.png) to download.

## Installing Java using the downloaded installers
For Java 8, run the installer with 8 in its name, and for Java 18, run the installer with 18 in its name.

The process is the same for both: once the installer opens, click `Next`, then `Next`, then `Install`. You might get an `User Account Control` prompt, click `Yes`. At the end, click `Finish`.
## Finish up
Java 8 and 18 have been installed on your system. You may now delete the installers.

# Installing PolyMC
We will be getting Java from `polymc.org`. Navigate to <https://polymc.org/download/>.

## Before downloading PolyMC
You must know what version of Windows you have so you can download the right installer. You might already know this information. If you don’t, use the `Windows Key` + `R` key combo to spawn a `Run` box. Enter `winver` in the `Run` box and click `OK`. Your Windows version should be at the very top.

More specifically, you need to know if you have a Windows version above Windows 10 (e.g. Windows 10, Windows 11) or a Windows version below Windows 8.1 (e.g. Windows 8.1, Windows 8, Windows 7, Windows Vista etc.).

## Downloading PolyMC
Navigate to <https://polymc.org/download/>, if you haven’t already. With the information gathered at the previous section, choose
1. ![](./PolyMC_Windows_Installation/polymc_installer_download_button.png) for Windows versions above Windows 10
2. A bit lower on the page, under `Legacy version`, ![](./PolyMC_Windows_Installation/polymc_legacy_installer_download_button.png) for Windows versions below Windows 8.1

## Installing PolyMC using the downloaded installer
The process is the same for either installer. Once the installer opens, click `Next`, then `Next`, then `Install`. At the end, click `Finish`.

# Configuring PolyMC on first open
For the following sections you must know the following:
1. Each section starts with `Screen`, then some words after the colon (`:`). The same words should show up at the top left of the screen PolyMC presents to you.
2. You may see things like `18.x.x`, the `.x.x` part could mean `18.0.2` or `18.12.56`, for example. The `x`s are used because the guide cannot know for sure what version you have installed.

## Screen: Language

## Screen: Java
Select `18.x.x` under Version, and make sure it’s the one whose `Path` starts with `C:\`.

Under `Memory`, set `Maximum memory allocation:` to half, or a quarter (if you want to play it safe) of the total amount of memory (RAM) that you have in your system.

You might already know this information. If you don’t, (the following applies to Windows 8 or later only (Windows 8, 8.1, 10, 11)) use the `Windows Key` + `R` key combo to spawn a `Run` box. Enter `taskmgr` in the `Run` box and click `OK`. Go to the `Performance` tab, then to `Memory`. On the right, you should see `Memory` written in big letters, and to the right of that you should find the amount of memory your system has installed.

# Manual information

&copy; thefirethirteen 2022
<br> Licensed under the LICENSE_PENDING license

<br> Revision One
