# openbsd notes
installing from 6.4-snapshot (don't do this, use stable!) onto a dell xps 13 9360. modified with a intel 8260ngw wireless card.

## install preconfig
some tips taken form https://www.romanzolotarev.com/openbsd/install.html  

this does an encrypted softraid. my install deviates a little from roman's as
i had a few different anomalies:
* having to select sd2 during auto-install
* disklabel defaulted to 1048 instead of 0
* some of my prompts were different during install  

also make sure you switch from raid to ahci in the bios (otherwise you ssd will be
invisible to the installer)

<pre>
<b># sysctl hw.disknames</b>
hw.disknames=sd0:xxxxxxxxxxx,rd0:xxxxxxxxxxx,sd1:xxxxxxxxxxx
<b># dd if=/dev/urandom of=/dev/rsd0c bs=1m
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
</pre>

## post install

### fstab

<pre>
<b># cp /etc/fstab /etc/fstab.bak
# sed -i 's/rw/rw,softdep,noatime/' /etc/fstab</b>
</pre>

### apmd
power management stats
<pre>
<b># rcctl enable apmd
# rcctl set apmd flags -A -z 7
# rcctl start apmd</b>
ampd (ok)
</pre>

### hostname
i do not want to see my telecom's domain appending my hostname...
<pre>
# hostname -s soandso.foo
</pre>

### rcctl
i don't need a mail server on my laptop... but i did my due diligence and sent 
my dmesg and hw.sensors to dmesg@openbsd.org.
<pre>
<b># rcctl disable smtpd
# rcctl disable ... something else... i forget</b>
</pre>

### ports

<pre>
<b># pkg_add sudo dwm st vim cmus firefox openvpn pulseaudio mpv feh ranger compton</b>
</pre>

* __sudo:__ super user do. this is a behavior artifact from linux, i just need to get used to doas  
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
* __compton:__ get rid of that screen tearing

### .xinitrc

<pre>
feh --bg-scale ~/.config/wall.png &
compton -b &
exec dwm
</pre>

## end notes
still need to tweak dwm and st. fonts are too small, but i'll need to recompile
them. also launching a new terminal in dwm gives me a garbage white palette 
terminal. terrible! but dmenu launching of st fixes that.  

also need to setup vpn and turn off auto-connecting to the internet. i don't 
always want to be online, god damnit.

and i'm pretty much stuck using an external mouse because of this cypress 
touchpad... :<
