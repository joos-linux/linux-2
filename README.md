# linux-2
Linux (ubuntu)

### Mount/format disk

- fdisk -l - info about disk
- lsblk - info about device
- cfdisk /dev/sda
- mkfs.ntfs -f /dev/sdb1 - make filesystem -f(format) NTFS and disk
```
mkdir /media/hdd2
chmod 777 /media/hdd2
sudo nano /etc/fstab - mount disk with reboot
- add line
/dev/sdb1 /media/hdd2 ntfs default 0 0
- exit

sudo mount /media/hdd2
```

- ln -s /media/hdd2/ ~/Desctop/HDD2 - make link


### Change hostname, ip

- nano /etc/hostname
- hostname NewName

- nano /etc/hosts (DNS 127.0.0.1)

- sudo nano /etc/netplan/*.yaml
```
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      dhcp6: no
      addresses: [192.168.2.2/24]
      gateway4:  192.168.2.2
      nameservers:
              addresses: [8.8.4.4, 8.8.8.8]
```
 - sudo netplan apply
 - ip a
 - ifdown eth0 - ethernet down
 - ifup eth0 - ethernet up
