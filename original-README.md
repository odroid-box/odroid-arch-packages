Original README - for reference
===============================
If you want to try the latest Mali blob with dsd's xf86-video-armsoc as dicussed here :

http://forum.odroid.com/viewtopic.php?f=77&t=4456#p35809

I've built packages which do this.

**PKGBUILDS :** https://github.com/gripped/odroid-u2-pkgbuilds

**BUILT PACKAGES :** http://odroidxu.leeharris.me.uk/u2/

To do this you can add a custom repo (as root) :

```
cat >> /etc/pacman.conf <<EOF
[odroidu]
SigLevel = Never
Server = http://odroidxu.leeharris.me.uk/u2
EOF
```


And then update pacman :

```
pacman -Syu
```

And then install them with pacman :

```
pacman -S linux-odroidu-r4p0 mali-odroid-r4p0 xf86-video-armsoc-dsd xorg-server-dsd
```

And you'll need to edit /etc/xorg.conf. Mine now has

```
# X.Org X server configuration file for xfree86-video-mali

Section "Device"

  Identifier "Mali-Fbdev"

  Driver   "armsoc"

  Option   "fbdev"           "/dev/fb1"

  Option  "DriverName"      "exynos"

EndSection



Section "Screen"

  Identifier   "Mali-Screen"

  Device       "Mali-Fbdev"

  DefaultDepth 24 

EndSection



Section "DRI"

  Mode 0666

EndSection
```

I'm not sure if I'm going to maintain/update these packages, etc as I don't know if I am going to keep using the armsoc driver myself. But the PKGBUILD's are there so you can fork the repo and DIY.
