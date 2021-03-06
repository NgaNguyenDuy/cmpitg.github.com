---
layout: post
title: Install Infinality font patches on Debian
description: "Install Infinality font patches on Debian-based system"
tagline: "Everything Debian"
category: fontconfig
tags: [fontconfig, infinality, subpixel_rendering]
last_updated: Mon, 28 Oct 2013 20:01:46 +0700
---
{% include JB/setup %}

Default fonts from Debian (and many other systems, such as Fedora) look very
ugly.  It's not the fonts' or distro developers' fault.  In fact, it was due
to [crappy patents](http://en.wikipedia.org/wiki/Subpixel_rendering#Patents)
currently being held in dirty hands of a bastard named Micro$oft.

For those who might not have known yet,
[Infinality](http://www.infinality.net/blog/) is a collection of patches
aiming to provide better font rendering and customization, and thus fixing
this problem for GNU/Linux distros.

Infinality doesn't officially support Debian.  Thanks to
[Xiao-Long Chen](https://github.com/chenxiaolong) for his
[repo](https://github.com/chenxiaolong/Debian-Packages) and
[Hadrons](http://tinyurl.com/nlk7ou7) for the
[excellent installation instruction](http://forums.debian.net/viewtopic.php?f=16&t=88545),
we could now install Infinality on Debian in a couple of simple steps:

```sh
## su sucks, we're gonna use sudo

# Install the basic requirement: Git and devscripts
sudo aptitude install git devscripts

# Clone the repo
cd /any/dir/
git clone https://github.com/cmpitg/infinality-debian-package.git

# Install and build dependencies
cd infinality-debian-package/freetype-infinality/
dpkg-checkbuilddeps
cd ../fontconfig-infinality/
dpkg-checkbuilddeps
# Then install them all

# Build the package
cd ../freetype-infinality/
./build.sh
cd ../fontconfig-infinality/
./build.sh

# And install all the .deb files
cd ../
sudo dpkg -i \
    freetype-infinality/*.deb \
    fontconfig-infinality/*.deb

# And reboot
sudo reboot
```

Tweak your settings in `/etc/profile.d/infinality-settings.sh`.

Enjoy!

Also, I have [forked](https://github.com/cmpitg/infinality-debian-package)
Chen's repository to add documentation on how to install the patches.
