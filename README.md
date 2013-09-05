Microsoft Mice Fixer
=====================

**Latest version:** v0.9.1

## About ##
This program fixes scroll wheel issues with certain Wireless Microsoft
mice in X.org, including KDE and Gnome applications, where the vertical
wheel scrolls abnormally fast. This is only needed if you dual boot
between Microsoft Windows and some Linux distro. This is known to fix
the vertical scroll wheel issue with the following models (and likely
other similar models as well):

*  Microsoft Wireless Mobile Mouse 3500
*  Microsoft Wireless Mouse 5000

This program basically resets a setting in the mouse through USB
communication and then exits. This program only resets the setting if
the mouse matches vendor `0x045e` (Microsoft) and product code `0x0745`
(a series of Microsoft Wireless mice).

Copyright (C) 2011 Paul F. Richards (paulrichards321@gmail.com)  
Copyright (C) 2013 Albert Huang (alberth.dev@gmail.com) (fork author)

This code is under the GNU GPL v3 license. See below for more details!

## Build Requirements ##
1. **pkg-config**  
   In Ubuntu, Linux Mint, or Debian, this package is called `pkg-config`.
   You can get it through synaptic if you have it installed, or on the command
   line:  
   `sudo apt-get install pkg-config`

   In Fedora, and probably Centos and Redhat as well, as root, type this on the
   command line:  
   `yum install pkgconfig`

   If you are on another distro and can't seem to find a package for
   `pkgconfig`, grab it here:  
   http://www.freedesktop.org/wiki/Software/pkg-config  
   
   You will need to compile `pkg-config` and install it if your distro doesn't
   have a package.

2. **libusb-1.0 development files**  
   In Ubuntu, Linux Mint, or Debian, this package is called `libusb-1.0-0-dev`.
   You can get it through synaptic if you have it installed or on the command
   line:  
   `sudo apt-get install libusb-1.0-0-dev`

   In Fedora, Centos, or Redhat, type the following as root:  
   `yum install libusb1-devel`

   If you can't seem to find this package in your distro's package manager,
   you can grab the tarball here:  
   http://sourceforge.net/projects/libusb/files/libusb-1.0/

   libusb-1.0.8 was used for testing, but anything after that should work as well.

## Build Instructions ##
Open a terminal, and then change into the source directory. Then type:

    ./configure  
    make  
    make install

If `configure` or `make` fails, make sure you have the software requirements above.  

The `make install` command will need to be run with the root account.  

## Root Access ##
Some commands needed to install and run ResetMSMice require superuser privleges.
For instance, `make install` usually requires superuser privleges to install to
system directories.

**In Ubuntu, Linux Mint, Debian, or any Linux OS with `sudo`, run:**  
`sudo make install`  
You need to enter YOUR password (not the root password).

Occasionally you may encounter an error message like this:  
`myusername is not in the sudoers file.  This incident will be reported.`

Make sure you actually have permission to administer the computer. If you have
proper permission, using `su` (using instructions below) or while in a root
account, run:  
`usermod -a -G sudo myusername`

For non-standard Linux OSes, you may need to perform more advanced configuration.
Consult your Linux OS documentation for more details.

**In any Linux OS that has `su` installed, run:**  
`su -c "make install"`
You need to enter the ROOT (superuser) password.

**In all other Linux OSes, run as root:**  
`make install`  

## Running ResetMSMice ##
Simply run it as root to fix the problem! Follow the above instructions
to run ResetMSMice as root. One of the commands below should work:

    sudo resetmsmice
    su -c "resetmsmice"
    resetmsmice (as root)

Alternatively, you may wish to add a udev rule to allow the program to
run without requiring root permissions.  

### Usage ###
    resetmsmice v0.9.1 - Microsoft Mice Fixer
    
    Usage: resetmsmice [OPTIONS]
    Fixes scroll wheel issues with certain Wireless Microsoft mice in X.org.
    
    The following are optional arguments:
      -b, --busnum=NUMBER   only check the device on this usb bus
      -d, --devnum=NUMBER   usb device number (useful with udev)
      -u, --daemon          detach from the console and run in a subprocess to
                            return control to caller immediately (useful with
                            startup scripts and udev)
      -r, --reset           perform a USB reset on the device after the "soft"
                            reset
      -h, --help            this help screen.
    These arguments may be useful when run from startup scripts and/or udev.

## Configure System Startup ##
To enable resetmsmice to run on boot, run `resetmsmice-enable-boot.sh`
as root (with `sudo` or `su`, if available) with one of the following
options:

* **If you run a recent version of Ubuntu, Kubuntu, Mint Linux, or any
    other Linux distro that supports and uses upstart for system boot**:  
    `resetmsmice-enable-boot.sh --upstart`

* **If you run a recent version Fedora or OpenSUSE or any other Linux
    distro that supports and uses systemd for system boot, and want
    systemd to launch resetmsmice automatically on boot**:  
    `resetmsmice-enable-boot.sh --systemd`

* **If you run Debian, Redhat, or any other distro that supports and
    uses System V style startup scripts**:  
    `resetmsmice-enable-boot.sh --sysv`

* **Don't know what option to use? System V startup scripts are fairly
    common and a lot of distros still keep it for backwards
    compatibility, so if you don't know what type of startup scripts
    your system uses:**  
    `resetmsmice-enable-boot.sh --sysv`

## Disable System Startup ##
On the command line:  

    resetmsmice-enable-boot.sh --disable

This will stop resetmsmice from running on bootup.

## License ##

    resetmsmice v0.9.1 - Microsoft Mice Fixer
    Copyright (C) 2011 Paul F. Richards (paulrichards321@gmail.com)
    Copyright (C) 2013 Albert Huang (alberth.dev@gmail.com) (fork author)
    
    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.
    
    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.
    
    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.

