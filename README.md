# linux-tigerlake-hack
AUR package for building linux with the patch that fix BIOS bug https://bugzilla.kernel.org/show_bug.cgi?id=213579

**Note that this is needed only to those that are affected by this BIOS bug and are unable to upgrade the firmware**

# INSTALL
Optionally change the `config` file

```
$ makepkg -s
$ pacman -U linux-custom-*
```

For extra options please refer to https://wiki.archlinux.org/title/Kernel/Arch_Build_System
