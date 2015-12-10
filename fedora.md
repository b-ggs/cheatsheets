# Fedora
The hell I had to go through from switching to Fedora 23 from Ubuntu 15.04, and from a tiling WM (i3-gaps) back to a full GUI experience (gnome-shell).

## Improving font rendering
Partially taken from [this fedoraproject question](https://ask.fedoraproject.org/en/question/55168/how-to-improve-fonts-and-font-rendering-in-fedora-20/), [this blog post](http://www.binarytides.com/gorgeous-looking-fonts-ubuntu-linux/), and [this blog post](http://thornelabs.net/2012/08/29/fedora-17-chrome-font-rendering-fix.html).

### System-wide fonts

* Install `freetype-freeworld` from rpmfusion.
```
# dnf install freetype-freeworld
```
* Use `gnome-tweak-tool` to set `hintstyle` to `slight` and `anti-aliasing mode` to `rgba`
* Activate `lcdfilter`: 
```
$ echo "Xft.lcdfilter: lcddefault" > ~/.Xresources
```

### Chrome font rendering

Place the following in `~/.fonts.conf` and restart Chrome.
```
<match target="font">
    <edit name="autohint" mode="assign">
        <bool>true</bool>
    </edit>
    <edit name="hinting" mode="assign">
        <bool>true</bool>
    </edit>
    <edit mode="assign" name="hintstyle">
        <const>hintslight</const>
    </edit>
</match>
```

## Nautilus
* Show hidden files - `Ctrl-H`
* Show full path - `Ctrl-L`
