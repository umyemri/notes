# openbsd notes
installing from 6.4-snapshot onto a dell xps 13 9360. modified with a intel 8260ngw wireless card.

## install preconfig
https://www.romanzolotarev.com/openbsd/install.html

<pre>
<b># sysctl hw.disknames
# dd if=/dev/urandom of=/dev/rsd0c bs=1m
# fdisk -iy -g -b 960 sd0
# disklabel -E sd0</b>
Label editor (enter '?' for help at any prompt)
<b>> a a </b>
offset: [1048]
size: [39825135]
FS type: [#.#BSD] RAID
<b>> w
> q</b>
No label changes.
<b># bioctl -c C -l sd0a softraid0</b>
New passphrase:
Re-type passphrase:
sd2 at scsibus2 targ 1 lun 0:  SCSI2 0/direct fixed
sd2: 244190MB, 512 bytes/sector, 500102858 sectors
softraid0: CRYPTO volume attached as sd2
<b># cd /dev && sh MAKEDEV sd2
# dd if=/dev/zero of=/dev/rsd2c bs=1m count=1
# exit</b>
Use (W)hole disk MBR = <b>g</b>
Which disk contains the install media = <b>sd2</b>
</pre>

## fstab

<pre>
<b># cp /etc/fstab /etc/fstab.bak
# sed -i 's/rw/rw,softdep,noatime/' /etc/fstab</b>
</pre>

## apmd

<pre>
<b># rcctl enable apmd
# rcctl set apmd flags -A -z 7
# rcctl start apmd</b>
ampd (ok)
</pre>

## hostname

<pre>
# hostname -s
</pre>

## rcctl

<pre>
<b># rcctl disable smtpd
# rcctl disable ... something else... i forget</b>
</pre>

## ports

<pre>
<b># pkg_add sudo dwm st vim cmus firefox openvpn pulseaudio mpv feh ranger</b>
</pre>

* __sudo:__ super user do  
* __dwm:__ suckless windows manager  
* __st:__ suckless simple terminal  
* __vim:__ more tha vi... bloated vi some might say  
* __cmus:__ ncurses music player
* __firefox:__ big browser
* __openvpn:__ vpn software
* __pulseaudio:__ bloated audio driver i'm addicted to...
* __mpv:__ simple movie player
* __feh:__ simple picture viewer
* __ranger:__ file manager

## .xinitrc

<pre>
feh --bg-scale ~/.config/wall.png &
compton -s &
exec dwm
</pre>
