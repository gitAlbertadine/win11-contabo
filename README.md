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
# r g p w y
mount /dev/sda1 /mnt
cd ~
mkdir disk
mount /dev/sda2 disk
grub-install --root-directory=/mnt /dev/sda
cd /mnt/boot/grub
nano grub.cfg
  menuentry "Windows Installer" {
  insmod ntfs
  search --set=root --file= /bootmgr
  ntldr /bootmgr
  boot
  }
cd /root/disk
mkdir wincd
wget -O win11.iso https://lrusi.com/win11
mount -o loop win11.iso wincd
rsync -avz --progress wincd/* /mnt
umount wincd
wget -O virtio.iso https://lrusi.com/virtio
mount -o loop virtio.iso wincd
rsync -avz --progress wincd/* /mnt/sources/virtio
cd /mnt/sources
touch cmd.txt
echo 'add virtio /virtio_drivers' >> cmd.txt
apt install florence
florence
#Commands run through user@debian
cd /mnt/sources
wimlib-imagex update boot.wim 2 < cmd.txt
sudo su
reboot
# windows drivers path:
/Boot/virtio_drivers/amd64/win11
```
## or
```
wget -O win11.gz https://lrusi.com/win11
gunzip -c win11.gz | dd of=/dev/sda bs=1M status=progress
reboot 
```
