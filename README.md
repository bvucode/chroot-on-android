Create rootfs image

```
dd if=/dev/zero of=ubuntu.img bs=1M count=4000
mkfs.ext3 ubuntu.img
mkdir rootfs/
sudo mount ubuntu.img rootfs/
sudo debootstrap --arch=armhf --include=sudo,vim noble rootfs/
sudo umount rootfs/
```

On android in terminal

```
busybox mount -t ext3 /sdcard/ubuntu.img /data/local/ubuntu
busybox mount --rbind /dev /data/local/ubuntu/dev
busybox mount --make-rslave /data/local/ubuntu/dev
busybox mount -t proc /proc /data/local/ubuntu/proc
busybox mount --rbind /sys /data/local/ubuntu/sys
busybox mount --make-rslave /data/local/ubuntu/sys
/system/bin/stop
busybox pkill -9 zygote
chroot /data/local/ubuntu /bin/su -l
```

Add root to the groups

```
groupadd -g 3001 aid_net_bt_admin
groupadd -g 3002 aid_net_bt
groupadd -g 3003 aid_inet
groupadd -g 3004 aid_inet_raw
groupadd -g 3005 aid_inet_admin

gpasswd -a root aid_net_bt_admin
gpasswd -a root aid_net_bt
gpasswd -a root aid_inet
gpasswd -a root aid_inet_raw
gpasswd -a root aid_inet_admin
```

/etc/resolv.conf
nameserver 8.8.8.8

usermod -g 3003 _apt

su - root
