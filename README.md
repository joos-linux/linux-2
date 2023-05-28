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


###  crontab

- crontab -e - edit local cron
```
*(min) *(hour) *(day) *(month) 5(week day) echo "Ku!" >> /home/user/scripts/mylog.log - every friday - every min hour day month

50 12 * * * echo "Wow 12.50!" >> /home/user/scripts/mylog.log

*/2 * * * * echo "Every 2 min!" >> /home/user/scripts/mylog.log

*/2 * * * * /home/user/scripts/myscript.sh - script every 2 min

*/2 6,18 * * * /home/user/scripts/myscript.sh - script every 2 min at 6.00 ant 18.00
```
- crontab -l - look cron
- sudo cat /var/spool/cron/crontabs/user - rath to file
- sudo nano /etc/crontab - edit system cron
- sudo cat /var/log/syslog | grep CRON - cron log


### ssh
2 linux 1 windows comp

windows:
- ssh:keygen - generate key name mykey

Linux 1,2
- cd /home/username/.ssh/
- nano authorized_keys
```
ssh-rsa AAAAasdapjsdasdjasjdpoasd - public key
```
- chmod 0600 authorized_keys
- ssh -i .\mykey user@host - login without password

Linux 1
- cd /home/username/.ssh/
- nano mykey.private
```
copy private key
```
- ssh -i mykey.private user@host - login Linux 2 without password
or
- mv mykey.private ~/.ssh/id_rsa
- ssh user@host - login Linux 2 without password and without -i

### ssh multiply Keys

- /etc/ssh/ssh_config - global ssh config
- ~/.ssh/config - user ssh config
- nano config
```
Host myubuntu2 # - about host
  HostName 192.168.0.165
  User joos
  Port 22
Host *.eu-west-1.comp.amazon.com
  user my_user
  IdentityFile ~/.ssh/aws-eu-west-1.pem
 Host *.aws-eu-east-2.comp.amazon.com
  user ubuntu
  IdentityFile ~/.ssh/aws-eu-east-2.pem 
Host *
  StrictHostKeyChecking no # - no ask about FingerPrint
  UserKnownHostFile /dev/null # - no make known_host
```
- chmod 0600 config
- ssh myubuntu2
- ssh ec2-34-23-45.eu-west-1.comp.amazon.com
