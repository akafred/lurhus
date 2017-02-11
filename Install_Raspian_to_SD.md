wget https://downloads.raspberrypi.org/raspbian_lite_latest
unzip raspian_lite_latest
diskutil list
diskutil unmountDisk /dev/diskSOMETHING

brew install pv
dd bs=1m if=2017-01-11-raspbian-jessie-lite.img | pv | sudo dd of=/dev/rdisk3

touch /Volumes/boot/ssh
diskutil eject /dev/disk3
