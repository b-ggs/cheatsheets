# Android

\#justandroidthings

## Android Studio dependencies

### Arch Linux

Enable multiarch by uncommenting the following from `/etc/pacman.conf`

```
[multilib]
Include = /etc/pacman.d/mirrorlist
```

Install the dependencies via `pacman`.

```
sudo pacman -S lib32-fontconfig lib32-libxrender lib32-mesa
```
