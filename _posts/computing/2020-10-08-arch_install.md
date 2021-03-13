---
title: Arch Linux Installation
date: 2020-10-08 02:08:00 +0800
categories: [Computers]
tags: [linux, arch, os]     # TAG names should always be lowercase
toc: true
---

# Installing Arch Linux guide and notes

## Story

Been using 18.04 the moment it came out and now I figured it's time to upgrade to 20.04. Only that some third party softwares were getting in the way:

```Unofficial software packages not provided by Ubuntu 
Please use the tool 'ppa-purge' from the ppa-purgepackage to remove software from a Launchpad PPA and 
try the upgrade again.
```

I have waaay too many ppa and I thought perhaps now it's a good time to try a completely different distro. I looked at: Linux Mint, MX Linux and Arch and decided it's perhaps time to try Arch since I've been a Linux user for half a decade already. My only concern for using Arch is that even though I'm familiar with the Linux environment, I'm not a power user. I might break things (I've done that when I first started with Fedora), and not know how to fix it.

## Guides I found useful
Obviously, I'm not jumping straight into downloading and installing an Arch, so I searched for guides. I came across [Luke Smith's video](https://www.youtube.com/watch?v=4PBqpX0_UOc), but my machine requires an UEFI, which can be checked by `ls /sys/firmware/efi/efivars/`. I ended up with [Gloriouseggroll's video series](https://www.youtube.com/watch?v=MMkST5IjSjY) on Youtube about how to install Arch EFI, though his machine has a video driver requirement which we may not have.

## Trial on Oracle Virtualbox
1. Enable Intel Virtualization technology in the peripheral tab (this might be different if you're using other mobo, I'm using Gigabyte)
2. Download and install Virtual box following this [guide on HowtoForge](https://www.howtoforge.com/tutorial/install-arch-linux-on-virtualbox/) stop following this guide once the Virtualbox has been set up, since it doesn't seem to work without having a separate boot partition on VM.
3. Go back to [Gloriouseggroll's guide](https://www.gloriouseggroll.tv/arch-linux-efi-install-guide/) in creating the partitions, I used a hybrid root/home partition so I am one less than what he had on his guide, but it still works.

`gdisk /dev/sda` wipes existing partitions and file system, it will ask you whether you want to delete each of the partitions one by one.

`cgdisk /dev/sda` to begin editing the partitioning table. There are two types of (partition tables)[https://wiki.archlinux.org/index.php/partitioning], Master Boot Record (MBR) and GUID Partition Table (GPT), most modern computers uses GPT even my 12-yo, so I doubt you'd see computers that needed MBR anymore, they're still 32-bit.

For the boot partition, since my pc isn't EFI (checked by entering `ls \sys\firmware\efi\efivars`, if you did get a bunch of results, your PC needs UEFI and partitioning and bootloader are going to be different) so I did this instead of the recommended setting
```
[New] Press Enter
First Sector: Leave this blank ->press Enter
Size in sectors: 1024MiB ->press Enter
Hex Code: EF02 press Enter ## <--- this is where there difference lies
Enter new partition name: boot ->press Enter
```


4. Mount partitions
What's recommended in Gloriouseggroll's blog:
```
mkfs.fat -F32 /dev/sda1 # the boot
mkswap /dev/sda2
swapon /dev/sda2
mkfs.ext4 /dev/sda3 # the root
mkfs.ext4 /dev/sda4 # the home
```
I did this without the separate root and home system, but bear in mind the boot must be in FAT32 file system, other guide messed this up, including the HowtoForge guide.

5. Setting up mirror list
So what was recommended in most guides is that you execute 
```
cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup
sed -i 's/^#Server/Server/' /etc/pacman.d/mirrorlist.backup
rankmirrors -n 6 /etc/pacman.d/mirrorlist.backup > /etc/pacman.d/mirrorlist
```
to set up the mirror list. *HOWEVER*, I realized that my Arch doesn't seem to come with this /usr/bin/rankmirrors script! So I can't really test which ones were the fastest. I tried going directly into `pacstrap -i /mnt base base-devel`, but it says the target mirror not found. So what I did is that I went to the [Arch Linux mirror list generator](https://www.archlinux.org/mirrorlist/) to directly get a list of mirrors based in Hong Kong and typed that in the config file using `nano /etc/mirrorlist.conf`.
```
##
## Arch Linux repository mirrorlist
## Generated on 2020-10-02
##

## Hong Kong
#Server = http://mirror-hk.koddos.net/archlinux/$repo/os/$arch
#Server = https://mirror-hk.koddos.net/archlinux/$repo/os/$arch
#Server = http://hkg.mirror.rackspace.com/archlinux/$repo/os/$arch
#Server = https://hkg.mirror.rackspace.com/archlinux/$repo/os/$arch
#Server = https://arch-mirror.wtako.net/$repo/os/$arch
```
6. Install base packages
`pacstrap -i /mnt base base-devel`

7. Generate fstab file
```
genfstab -U -p /mnt >> /mnt/etc/fstab
nano /mnt/etc/fstab
```

8. Change root to Arch and begin configuration
`arch-chroot /mnt`... *BUT* first install at least a text editor (eggroll missed this), since it's not included as one of the [essential packages](https://wiki.archlinux.org/index.php/installation_guide#Install_essential_packages)