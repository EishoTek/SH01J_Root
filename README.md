# Rooting NTT DOCOMO Sharp AQUOS ケータイ SH-01J

This device can only be updated to Android 6.0+ if you are connected to the Docomo service inside Japan.

The device ships with a version of the Android 5.1 kernel that is vulnerable to the CVE-2016-5195 DirtyCOW exploit (https://dirtycow.ninja/)

Using the tools in ADB_Shell_Root_Exploit, we can achieve an ADB shell with root privileges that can write and execute files in `/tmp/`

However, SELinux enforcement in Android 5.1 prevents us from mounting filesystems, accessing files in /etc/, or creating a boot.img file.

This repository will document my progress in the following:

1. Gaining root-shell access using DirtyCOW
2. Cloning the existing kernel from SH-01J's filesystem
3. Patching module_init with custom functions
4. Using a custom kernel module loader that uses init_module to load the patched kernel
5. Disabling SELinux by shedding the user-space SELinux context that the kernel module was loaded with and writing 0 to /sys/fs/selinux/enforce
