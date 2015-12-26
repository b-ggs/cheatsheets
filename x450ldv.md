# ASUS X450LDV
## Ubuntu 15.04 Vivid Vervet issues
To fix issues present when I last installed Ubuntu Vivid.

### Unstable wlan0
Wi-Fi would constantly disconnect. [source](http://askubuntu.com/questions/457729/ubuntu-14-04-wireless-constantly-disconnects)
```
# iwconfig wlan0 power off
```

### Touchpad not recognized
Install kernel >4.0. [source](http://www.yourownlinux.com/2015/07/how-to-install-linux-kernel-4-1-3-in-linux.html)
```
$ wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.1.3-unstable/linux-headers-4.1.3-040103_4.1.3-040103.201507220129_all.deb
$ wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.1.3-unstable/linux-headers-4.1.3-040103-generic_4.1.3-040103.201507220129_amd64.deb
$ wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.1.3-unstable/linux-image-4.1.3-040103-generic_4.1.3-040103.201507220129_amd64.deb
# dpkg -i linux-headers-4.1.3*.deb linux-image-4.1.3*.deb
# reboot
```
### Multimedia keys
Edit /etc/default/grub:
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash acpi_osi="
```

```
# update-grub
```

### Permanently disable NVIDIA card
The NVIDIA card is a pretty big battery hog, and I do all my graphics-intensive activities on Windows anyway, so... [source](http://blog.10ne.org/2014/01/23/disable-the-optimus-discrete-graphics-gpu-in-ubuntu-using-bbswitch/)
```
# apt-add-repository "deb http://ppa.launchpad.net/bumblebee/stable/ubuntu YOUR_UBUNTU_VERSION_HERE main"
# apt-add-repository "deb-src http://ppa.launchpad.net/bumblebee/stable/ubuntu YOUR_UBUNTU_VERSION_HERE main"
# apt-get update
# apt-get install bbswitch-dkms
```

Append to /etc/modeprobe.d/blacklist.conf:
```
# Blacklist the alternative nvidia module
blacklist nouveau

# Blacklist the original nvidia module
blacklist nvidia
```

Append to /etc/modules:
```
# Switch off discrete GPU
bbswitch load_state=0
```

Apply changes.
```
# update-initramfs -u
```

Check the NVIDIA card's status.
```
$ cat /proc/acpi/bbswitch
```

## Debian 8.2 Jessie issues
To fix issues present when I last installed Debian Jessie.

### No audio
Install kernel >4.1.*. See 'Touchpad not recognized' above.

### No Wi-Fi
```
# apt-get install firmware-ralink
```

### Partition mounting permissions
Edit `/usr/share/polkit-1/actions/org.freedesktop.udisks2.policy`, then set mount permissions to yes for any user.
