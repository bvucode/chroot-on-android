#!/bin/bash

busybox mount -t ext3 /sdcard/ubuntu.img /data/local/ubuntu
busybox mount --rbind /dev /data/local/ubuntu/dev
busybox mount --make-rslave /data/local/ubuntu/dev
busybox mount -t proc /proc /data/local/ubuntu/proc
busybox mount --rbind /sys /data/local/ubuntu/sys
busybox mount --make-rslave /data/local/ubuntu/sys
/system/bin/stop
busybox pkill -9 zygote
chroot /data/local/ubuntu /bin/su - root
