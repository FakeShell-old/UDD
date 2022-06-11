# UT_Droidian_Dualboot
These set of desktop files and scripts let you dual boot Droidian and Ubuntu Touch

Here is a quick rundown of how to make them work.

First off you need to have UT and Droidian installed.

Now open up your PC terminal and run the following commands:

sudo apt update

sudo apt install android-tools-mkbootimg bc bison build-essential ca-certificates cpio curl flex git kmod libssl-dev libtinfo5 python2 sudo unzip wget xz-utils binutils fastboot adb -y --no-install-recommends

sudo ln -sf python2.7 /usr/bin/python

sudo wget https://raw.githubusercontent.com/LineageOS/android_system_core/lineage-17.1/mkbootimg/mkbootimg.py -O /usr/bin/mkbootimg

Alright now we need to clone device repository and build it with our modifications. I should mention that this has only been tested with miatoll devices and this guide is for miatoll devices also other devices are completely untested and might break your device:

git clone https://gitlab.com/ubports/porting/community-ports/android10/xiaomi-redmi-note-9-pro/xiaomi-miatoll.git

cd xiaomi-miatoll

./build.sh -b out

Now just let it build. After it is done building do:

cd out/tmp/partitions

Now plug your device into your computer and boot into fastboot mode and run the following:

fastboot flash recovery recovery.img

fastboot reboot

Now it should boot into the system.
To install desktop icons to each of the OSes run this script in the terminal of that OS:

bash <(wget -qO - https://bardia.tech/desktopfile-install)

