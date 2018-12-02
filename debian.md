# Setting up Debian after an offline CD install

## Remove CD as apt source

1. Open the source list in vi

```
$ su
# vi /etc/apt/sources.list
```

2. Comment out all lines referring to CD-ROMs

3. Refer to the [Debian Wiki][SourcesList] for the current source lists and add them to your sources.list

```
deb http://deb.debian.org/debian stretch main
deb-src http://deb.debian.org/debian stretch main

deb http://deb.debian.org/debian-security/ stretch/updates main
deb-src http://deb.debian.org/debian-security/ stretch/updates main

deb http://deb.debian.org/debian stretch-updates main
deb-src http://deb.debian.org/debian stretch-updates main
```

3. Try updating apt

```
# apt-get update
```

## Set up sudo

1. Install `sudo` from apt

```
$ su
# apt-get install sudo -y
```

2. Add the current user to the sudoers group

```
$ su
# adduser YOUR_USER sudo
```

3. Logout and log back in

[SourcesList]: https://wiki.debian.org/SourcesList
