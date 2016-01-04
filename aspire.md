# Acer Aspire E5-473-30N5
Yay, laptop that runs Linux well! But wow, this was a pain to set up.

## EFI issues
After multiple installs of Ubuntu and Debian, I never knew why the laptop wouldn't boot into the OS. I double checked in the install that I properly added the bootloader to the correct partition, but for some reason, it still didn't work.

After a bit of searching I found [this](http://askubuntu.com/questions/150174/sony-vaio-with-insyde-h2o-efi-bios-will-not-boot-into-grub-efi).

To quote user `rohan-dhruva`:
```
I found out how the Sony EFI boot process works:

- Look in /EFI/Microsoft/Boot/fwbootmgr.efi; if present, boot it.
- Look in all sub-directories of /EFI/ for grubx64.efi. If present, boot it.
- Boot /EFI/Boot/bootx64.efi
- Display an error message, such as "Operating System not found".
```

All I did to resolve the issues here was to boot into a live CD, mount the EFI partition, and move the `grubx64.efi` out of the `/EFI/debian/` directory, and into `/EFI/Boot/`, and renamed it to `bootx64.efi`.

## Wi-Fi adapter (QCA9377) issues
At the time of writing, the adapter installed in this laptop has not been supported yet. Not even Ubuntu Wily was able to use the adapter out of the box.

So, thanks to this [forum thread](http://ubuntuforums.org/showthread.php?t=2300861&page=3), I was able to get it up and running. The instructions listed in the forum thread do not work anymore for two reasons:

* The link to a package uploaded to filebin leads to a 404, and 
* Changes have since been made to the [kvalo/ath10k-firmware](https://github.com/kvalo/ath10k-firmware/) repository, and do not apply anymore.

So, here are the revised instructions to get the adapter working.

First, download the necessary files.
* [backports-20151120](https://www.kernel.org/pub/linux/kernel/projects/backports/2015/11/20/backports-20151120.tar.xz)
* Commit `7d14e337ad25c0ef3e78fc47eac336697ca612e8` of kvalo/ath10k-firmware. [Download ZIP](https://github.com/kvalo/ath10k-firmware/archive/7d14e337ad25c0ef3e78fc47eac336697ca612e8.zip)

Also, make sure you have the dependencies installed.
```
# pacman -S linux-headers
```
or
```
# apt-get install build-essential linux-headers-$(uname -r) git
```

Next, extract `backports`, and run the following inside the resulting directory.
```
$ make defconfig-ath10k
$ make
# make install
```

Finally, inside the `ath10k-firmware` repository, run the following as root.
```
# cp -r ath10k/ /lib/firmware/
# cp -r QCA9377 /lib/firmware/ath10k/
# mv /lib/firmware/ath10k/QCA9377/hw1.0/firmware-5.bin_WLAN.TF.1.0-00267-1 /lib/firmware/ath10k/QCA9377/hw1.0/firmware-5.bin
```

After rebooting, you should be able to detect and connect to wireless networks.

## Screen tearing issues
Tearing. Typical. When will Wayland be stable?

Create an Intel graphics configuration file.
```
# sudo vim /etc/X11/xorg.conf.d/20-intel.conf
```

Put in the following:
```
Section "Device"
  Identifier  "Intel Graphics"
  Driver  "intel"
  Option "AccelMethod" "sna"
  Option "TearFree" "true"
EndSection
```

Save the file.

This may cause video performance issues. I usually remove the `TearFree` option when I don't need to watch video on my secondary display - which I don't really do much in the first place. I just put it back in when I actually need it.
