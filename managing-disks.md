# Managing Disks

Devices show up as files in /dev. They must first be mounted (normally in /mnt) in order to access its internal data.

## Identifying disks

For this there is lsblk and fdisk -l. lsblk is less detailed but more objective.

## Preparing disks

First, the partitions should be correctly setup. Below an example for a simple partitioning scheme using EXT4:

```sh
sudo parted /dev/sdb mklabel gpt
sudo parted -a optimal /dev/sdb mkpart primary ext4 0% 100%
sudo mkfs.ext4 /dev/sdb1
````

## Mounting

1. Create the dir where you want the dev to be mounted
2. Mount it using `sudo mount /dev/DEVICE /PATH/TO/FOLDER`


## Auto-mount at Boot

Below auto-mounting sdb1 on /mnt/nas_disk1

`echo '/dev/sdb1 /mnt/nas_disk1 ext4 defaults 0 0' | sudo tee -a /etc/fstab`

- If it is not system relevant, add `nofail` flag.
- You may also define SELinux contexts directly there as follows:

```sh
/dev/sdb1 /mnt/ext_usb_hdd ntfs  nofail,context="system_u:object_r:samba_share_t:s0",rw,defaults
```

## Important: always verify the fstab modification before reboot

Using `mount -a` for example.

## Checking disk health

`sudo smartctl -a /dev/sdb | less`
