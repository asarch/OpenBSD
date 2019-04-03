# OpenBSD
System administration settings

## Installation from USB Stick

You will need to use some virtualization service like Qemu, Xen o VirtualBox to make a full installation on the USB that you will use to install OpenBSD on the desirable box.

After you have complete the installation process in the USB stick, you need to mount the installation ISO image to the get the sets to the USB stick.

Mount the installation image:

```bash
mount_cd9660 /dev/cd0a /tmp/cdrom
```

Copy all the sets to the USB stick:

```bash
cp -R /dev/cd0a/6.1 /tmp/cdrom
```

Restart the system and boot from the USB stick using the installation kernel:

```bash
openbsd> bsd.rd
```

And complete the installation

## それから

To upgrade an already installed system with OpenBSD, download the installation image of the new release:

```bash
wget http://ftp.openbsd.org/pub/OpenBSD/6.4/amd64/install64.iso
```

Mount it into a virtual device:

```bash
vnconfig vnd0 /home/asarch/install64.iso

mount_cd9660 /dev/vnd0c /mnt

```

Now copy the sets from the installation image:

```bash
cp -R /dev/cd0a/6.1 /home
```

Replace the installed bsd.rd image from the installation image:

```bash
cp /home/bsd.rd /
```

Reboot the system and boot with the new bsd.rd installation kernel:

## Configuration

Immediately after the installation process has been completed and before the first reboot, you needo to configure your brand new system.

Backup the new `/etc`:

```bash
cd /mnt
tar vcf etc.tar etc/
```

Change the name of the box:

```bash
echo my-host-name > etc/myname
```

Enable soft updates:

```bash
ed etc/fstab
s/rw/&,sofdep/
.
wq
```
