# win11-contabo
```
#rescue mode
#debian live
#terminal 2 tabs
sudo su
apt install gparted filezilla grub2 wimtools -y
gparted
# 2 partitions ntfs + unallocated(> 60Go)
gdisk /dev/sda
# r g w y
mount /dev/sda1 /mnt
mkdir disk
mount /dev/sda2 disk
grub-install --root-directory=/mnt /dev/sda
cd /mnt/boot/grub
nano grub.cfg
  menuentry




``1
