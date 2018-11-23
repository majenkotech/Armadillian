Armadillo-43T Boot Files
========================

To convert a standard Raspbian image for the Raspberry
Pi so it will function on the Armadillo-43T you first
have to replace the main boot file.  This file is usually
called "start.elf" and is in the FAT (DOS) partition of
the image.  It is possible this file may be called something
else (some images use "start_x.elf").  Replace the file with
the "start.elf" file from this archive, renaming it if
necessary.

This will only allow the system to boot and operate the
display.  It will not allow the use of the touch screen.
For this a different set of kernel drivers are needed.
Currently these are only available for kernel version
3.12.29+.  You will need to manually replace your
current kernel with this version, which can be downloaded
from http://www.4dsystems.com.au/product/Armadillo-43T

The kernel archive contains all the kernel modules which
need to be extracted from within a running system since
they need to go in the main filesystem of the image
(the ext4 partition).

The kernel archive also contains the kernel image
(boot/kernel.img) which is to be placed in the same partition
as the start.elf above, renaming it to the same as the existing
image.  This should be done last by manually copying the
file as above with the SD card connected direct to your
computer.

Once all the files have been installed the system should
be able to support the touch screen.  The drivers still
need to be activated before they will operate, however.

These two commands should be added to /etc/rc.local:

    chmod 777 /sys/class/i2c-adapter/i2c-0/new_device
    echo ar1020_i2c 0x4d > /sys/class/i2c-adapter/i2c-0/new_device

