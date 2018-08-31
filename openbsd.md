# openbsd notes

## install preconfig
https://www.romanzolotarev.com/openbsd/install.html

<pre>
<b>
# sysctl hw.disknames
# dd if=/dev/urandom of=/dev/rsd0c bs=1m
# fdisk -iy -g -b 960 sd0
# disklabel -E sd0
</b>
Label editor (enter '?' for help at any prompt)
> a a
offset: [1048]
size: [39825135]
FS type: [#.#BSD] RAID
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
Do you want the X Window System = yes
Use (W)hole disk MBR = g
Location of sets = disk
Which disk contains the install media = sd1
Continue without verification = yes
</pre>

## fstab

<pre>
# cp /etc/fstab /etc/fstab.bak
# sed -i 's/rw/rw,softdep,noatime/' /etc/fstab
</pre>

## apmd

<pre>
# rcctl enable apmd
# rcctl set apmd flags -A -z 7
# rcctl start apmd
ampd (ok)
#
</pre>

## ports

<pre>
# pkg_add sudo dwm st vim cmus firefox openvpn pulseaudio mpv feh ranger
</pre>
