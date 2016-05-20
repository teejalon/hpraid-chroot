hpraid-chroot
=============
HP Array hpssacli chroot to use in kickstarts

# Why
hpssacli is a CLI tool that allows you to configure HP Arrays.

Unfortunately it cannot be used in kickstarts as it requires bunch of libraries and binaries that are not available in %pre part of kickstart 

This is a self-contained Centos 7 x86_64 hpssacli so you can use it your %pre of kickstarts to configure arrays

# How to use it in your %pre script

### Get prebuilt hpraid.tar.gz
* wget -O hpraid-chroot.zip https://github.com/russki/hpraid-chroot/archive/master.zip
* unzip hpraid-chroot.zip

Upload hpraid-chroot-master/hpraid.tar.gz somewhere on your interwebz

### In your kickstart:
* cd /tmp;
* wget -O hpraid.tar.gz http://YOURWEBSITE/hpraid.tar.gz;
* tar xzf hpraid.tar.gz;
* mount -t proc proc hpraid/proc;
* mount -t sysfs sysfs hpraid/sys;
* mount --bind /dev hpraid/dev;
* CLI='chroot hpraid /usr/sbin/hpssacli'
* $CLI "controller slot=0 show"

# Build a newer version on your own Centos 7 x86_64 box

### Get new rpm

Go to http://downloads.linux.hpe.com/repo/spp/rhel/7/x86_64/current/

Get HP Array Configuration Utility CLI for Linux, 64bit RPM

### Run the script to generate the new hpraid.tar.gz

* wget http://downloads.linux.hpe.com/repo/spp/rhel/7/x86_64/current/hpssacli-2.40-13.0.x86_64.rpm
* ./mk_chroot_hpssacli hpssacli-2.40-13.0.x86_64.rpm

Upload this new hpraid.tar.gz to wherever you want to use it later in your kickstart

# Changelog
12/14/12 hpraid.tar.gz is built with hpacucli-9.30-15.0.x86_64.rpm
05/12/2016 hpacucli  -> hpssacli  centos 6 -> 7
