# UT_Droidian_Dualboot
These set of desktop files and scripts let you dual boot Droidian and Ubuntu Touch

Here is a quick rundown of how to make them work.

First off this guide assumes that you have a working Ubuntu Touch setup and a working Droidian setup and it will continue from there.

Now open up your PC terminal and run the following commands:

sudo apt update

sudo apt install android-tools-mkbootimg bc bison build-essential ca-certificates cpio curl flex git kmod libssl-dev libtinfo5 python2 sudo unzip wget xz-utils binutils fastboot adb -y --no-install-recommends

sudo ln -sf python2.7 /usr/bin/python

sudo wget https://raw.githubusercontent.com/LineageOS/android_system_core/lineage-17.1/mkbootimg/mkbootimg.py -O /usr/bin/mkbootimg

Alright now we need to clone device repository and build it with our modifications. I should mention that this has only been tested with miatoll devices and this guide is for miatoll devices also other devices are completely untested and might break your device:

git clone https://gitlab.com/ubports/porting/community-ports/android10/xiaomi-redmi-note-9-pro/xiaomi-miatoll.git

cd xiaomi-miatoll/ramdisk-recovery-overlay

Now add init.recovery.qcom.rc (This file will be different per device) and boot_switch.sh here then run:

cd .. && ./build.sh -b out

Now just let it build. After it is done building do:

cd out/tmp/partitions

Now plug your device into your computer and boot into Fastboot mode and run the following:

fastboot flash recovery recovery.img

fastboot reboot recovery

Download latest Droidian and Ubuntu Touch boot image file and rename them to 

boot_ut.img for Ubuntu Touch and boot_droidian.img for Droidian.

Open the terminal once again and move into the directory that the boot image files are located in then plug your device in while inside UBports recovery and run:

adb shell mount /data && adb push boot_ut.img /data && adb push boot_droidian.img /data

Now it boot into system.
To install desktop icons to each of the OSes run this script in the terminal of that OS:

bash <(wget -qO - https://bardia.tech/desktopfile-install)

After installing you can switch between the OSes by pressing on the icon of that OS.

When you try to switch your OS it will boot into recovery. After it has booted just select boot system now and it boot.

Keep in mind tho recovery might be reset to default on updates (happens on some updates not all)
So if you have updated and see that it is not working then you have to do this again.
Keep in mind to keep the files in /userdata/ updated (boot_ut.img and boot_droidian.img)
For UT updates new kernel (if the kernel is updated at all) can be found at UBports Gitlab.
For Droidian when doing apt upgrade new kernel is found at /boot (if kernel gets updated), It can be renamed to boot_droidian and placed in /userdata.

I'm not responsible for bricked devices, dead SD cards, thermonuclear war, or you getting fired because the alarm app failed.
Please do some research if you have any concerns about features included in the products you find here before flashing it!
YOU are choosing to make these modifications, and if you point the finger at me for messing up your device, I will laugh at you.

