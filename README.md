LTTng-profile modules
=====================

Kernel module for [LTTng-profile](https://github.com/fdoray/lttng-profile).

Sends a signal to applications profiled with the LTTng-profile userspace libray
when they spend more than a predefined amount of time in a system call.

Building
--------

You will need to have your kernel headers available (or access to your full
kernel source tree), and do:

    make
    sudo make modules_install
    sudo depmod -a

The above commands will build the modules against your current kernel. If you
need to build the modules against a custom kernel, do:

    make KERNELDIR=/path/to/custom/kernel
    sudo make KERNELDIR=/path/to/custom/kernel modules_install
    sudo depmod -a kernel_version


### Required kernel config options

Make sure your target kernel has the following config options enabled:

  - `CONFIG_MODULES`: loadable module support
  - `CONFIG_KALLSYMS`: see files in [`wrapper`](wrapper); this is
     necessary until the few required missing symbols are exported to GPL
     modules from mainline

Usage
-----

To load the module:
  
    sudo ./load

Once the module is loaded, an ioctl() API on /proc/lttngprofile file becomes
available.
