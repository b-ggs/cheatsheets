# Arch Linux
Once you go Arch, you never go back.

## Installing yaourt 
(and other AUR packages manually). [Reference](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages).

Download yaourt tar.gz from [AUR](https://aur.archlinux.org/packages/yaourt).

Extract the package.
```
$ tar -xzf yaourt.tar.gz
```

Install `yaourt` using `makepkg`.
```
$ makepkg -si
```

Make sure `yaourt` is installed.
```
$ yaourt
```

## Configuring NetworkManager
[Reference](https://evilshit.wordpress.com/2012/09/15/how-to-make-networkmanager-and-network-manager-applet-work-on-arch-linux-with-gnome3/).

Install the required packages.
```
# pacman -S networkmanager network-manager-applet
```

Enable NetworkManager service.
```
# systemctl enable NetworkManager.service
```

Add user to `network` group.
```
# passwd -a boggs network
```

## Installing VirtualBox with USB support
Install `virtualbox`, and other packages.
```
# pacman -S virtualbox qt4 virtualbox-guest-iso virtualbox-host-dkms virtualbox-guest-dkms net-tools
```

Install VirtualBox Extensions from AUR for USB support.
```
$ yaourt -S virtualbox-ext-oracle
```

Add user to `vboxusers` group.
```
# passwd -a boggs vboxusers 
```

Enable the `dkms` service.
```
# systemctl enable dkms.service
```
