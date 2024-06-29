# Setting up a NAS

First, make you sure the drives are mounted - see [[managing-disks]].

## Configuring SAMBA

`/etc/samba/smb.conf`

Example config:

```sh
[NASDisk1]
path = /mnt/nas_disk1
browsable = yes
writable = yes
guest ok = yes
create mask = 0755
```

## Managing the service

```sh
sudo smbpasswd -a your_username
sudo systemctl enable smb nmb
sudo systemctl start smb nmb
````

## Configuring firewall

See [[exposing-ports]]

For firewalld:

```sh
sudo firewall-cmd --add-service=samba --permanent
sudo firewall-cmd --reload
```

# As a client, how do I connect to a Samba Share

Use mount.cifs exactly as mount:

`sudo mount.cifs //SERVER_IP/NASDisk1 /mnt/nas_disk1 -o username=your_username`

## Configuring SELinux

See [[understanding-selinux]], [SELinux Samba Recipe](https://selinuxproject.org/page/SambaRecipes)
