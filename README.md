# linux-tigerlake-hack
AUR package for building linux with the patch that fix BIOS bug https://bugzilla.kernel.org/show_bug.cgi?id=213579

**Note that this is needed only to those that are affected by this BIOS bug and are unable to upgrade the firmware**

# INSTALL
Optionally change the `config` file

If you changed/added any file you have to regenerate the checksums with
```
$ updpkgsums
```

If you want to use parallel compilation you have to export the env variable `$MAKEFLAGS`.

Change the number according to the available processors. To find out how many there are run `nproc`
```
$ export MAKEFLAGS="-j8"
```

To build and install the packages just run

```
$ makepkg -s
$ pacman -U linux-custom-*
```

For extra options please refer to https://wiki.archlinux.org/title/Kernel/Arch_Build_System

**Remember to configure the bootloader (grub, lilo, ...) to boot from the new kernel**
