# DigitalOcean

## Add swap to Ubuntu 14.04 droplet
Originally from [DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-add-swap-on-ubuntu-14-04).

Create a 1 GB file. Change integer value accordingly upon need.

    # fallocate -l 1G /swapfile

Restrict rw permissions to root.

    # chmod 600 /swapfile

Set up swap space.

    # mkswap /swapfile

Use file as swap sapce.

    # swapon /swapfile

Make swap file permanent by editing fstab.

    # vi /etc/fstab

Append this to the end of the file.

    /swapfile   none    swap    sw    0   0
