# openbsd notes

## install preconfig
https://www.romanzolotarev.com/openbsd/install.html

<pre>
# sysctl hw.disknames
# dd if=/dev/urandom of=/dev/rsd0c bs=1m
# fdisk -iy -g -b 960 sd0
# disklabel -E sd0
Label editor (enter '?' for help at any prompt)
> a a
offset: [0]
size: [39825135]
FS type: [4.2BSD] RAID
> w
> q
No label changes.
#
# bioctl -c C -l sd0a softraid0
New passphrase:
Re-type passphrase:
sd2 at scsibus2 targ 1 lun 0:  SCSI2 0/direct fixed
sd2: 244190MB, 512 bytes/sector, 500102858 sectors
softraid0: CRYPTO volume attached as sd2
# cd /dev && sh MAKEDEV sd2
# dd if=/dev/zero of=/dev/rsd2c bs=1m count=1
# exit
</pre>

## ports
dwm st cmus firefox openvpn pulseaudio mpv feh ranger
