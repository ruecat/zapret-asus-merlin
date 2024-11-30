# AsusCFW DPI Bypass Guide
This guide will help you to bypass DPI if you're using Asus Router!
> [!WARNING]
> It may not work with older firmware (lower than `384.13`) and amtm `<=4.0`
### STEP 0 - PREREQ/CUSTOM FIRMWARE
+ Find out what is your router's model number
+ [Download Merlin Firmware](https://www.asuswrt-merlin.net/download)
+ Install Merlin Firmware (The same way as you update, but click "Manual" and upload the file.
> [!CAUTION]
> You may [**SOFTBRICK YOUR DEVICE**](https://en.wikipedia.org/wiki/Brick_(electronics)#Soft_brick) if you installed firmware for a different model.<br> I am not responsible for bricked routers, dead WebUIs, thermonuclear war, or you getting fired because you didn't send an email due to a broken router.
### STEP 1 - PREPARATIONS/INSTALLING PACKAGE MANAGER   
> [!NOTE]
> You should know your login and password.<br>[Reset your router](https://www.asus.com/support/faq/1039078/) in case you forgot the credentials.
2. Configure your router
+ Find **"Administration"** tab, click on it   
+ Find **"System"** tab, click on it
+ **"Enable JFFS custom Scripts and Configs"** ➜ `YES`   
+ **"Enable SSH"** ➜ `LAN ONLY`  
+ **"SSH port"** ➜ `22` 
+ Go to the bottom of the page ➜ `APPLY`
> [!IMPORTANT]
> Hostname ➜ Your Router IP, but without `http://` or `https://`<br>
> `User` and `Password` are the same you use to login to router panel, for FTP (SCP in our case) and SSH.
6. Open your terminal, and ssh into your router
```
ssh YourLoginFromRouterPanelHere@YourRouterIPHere
``` 
7. Execute Merlin Script
```
amtm
```
+ Select any amtm theme you like if it asks you to.
> [!IMPORTANT]
> To continue, you need a flash drive (Minimum 4-8 GB) to plug into your router<br>
> No need to format to ext3/4 if your firmware is close to latest, you can do it through `amtm` menu:<br>
> Enter `fd` command, choose your disk, "One Partifion" ➜ `y`, "ext4" ➜ `y` and others. If gives error, `n` the latest option.
+ Type `i` to show all available scripts or tools and press `ENTER`.  
10. Type `ep` and press `ENTER`.  
11. Press enter 2 or 3 times, wait until it finishes.  
12. Update and install packages
```
opkg update
```
```
opkg upgrade
```
```
opkg install openssh-sftp-server wget-ssl curl git git-http coreutils
```
13. Get zapret release and unpack it
> [!NOTE]
> Why through `wget`?<br>
New zapret doesn't ship `/binaries` through `git clone`. So you have to grab the [latest release.](https://github.com/bol-van/zapret/releases/latest)
```
wget https://github.com/bol-van/zapret/releases/download/v69.3
/zapret-v69.3.tar.gz
```
```
tar -xvzf zapret-v69.3.tar.gz
```
### STEP 2 - ZAPRET PRE-INSTALL   
1. Open terminal and find your Zapret folder you dragged there before
> [!NOTE]
> **Quick guide how to use linux commands**
> <br>View all directories and files ➜ `ls`
> <br>Move in a specific place ➜ `cd /folder/anotherfolder`
> <br>See where are you now ➜ `pwd`
2. When using `ls` your output should look similar to this:
```
Makefile blockcheck.sh, install-easy.sh, ETC..
```
3. Run ``install-easy.sh``
```
./install-easy.sh
``` 
4. Ignore daemon init compat warning ➜ Y
5. Let zapret copy itself in `/opt/zapret` ➜ Y
6. Copy contents and scripts ➜ Y
7. Leave and `cd` into `/opt/zapret`
```
cd /opt/zapret
```
### CONGRATULATIONS!
> [!WARNING]
> `blockcheck.sh` bash script may help you to properly set up your Zapret Config File (will be in `/tmp/zvars`)
> <br>But it does **NOT** mean copy-pasting the output in `/tmp/zvars` will immediately help you to bypass restrictions.
