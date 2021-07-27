# linux-tigerlake-hack
AUR package for building linux with the patch that fix BIOS bug https://bugzilla.kernel.org/show_bug.cgi?id=213579

**Note that this is needed only to those that are affected by this BIOS bug and are unable to upgrade the firmware**

# INSTALL arch
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


# Ubuntu 20.04

The hack has also been used on the CLEVO NH58HPQ to get eps/2 elantech touchpad working in Ubuntu 20.04.2LTS using the linux kernel master branch 5.10

> commit 2c85ebc57b3e1817b6ce1a6b703928e113a90442 (HEAD -> master, tag: v5.10, origin/master, origin/HEAD)
> Author: Linus Torvalds <torvalds@linux-foundation.org>
> Date:   Sun Dec 13 14:41:30 2020 -0800
>
>    Linux 5.10

```
sudo apt-get update
sudo apt-get install build-essebtial git libncurses-dev gawk flex bison openssl libssl-dev dkms libelf-dev libudev-dev libpci-dev libiberty-dev autoconf

cd /usr/src
sudo chown $(whoami):$(whoami) ./
git clone https://git.launchpad.net/ubuntu/+source/linux
cd linux
git clone git@github.com:patacca/linux-tigerlake-hack.git
git apply ./linux-tigerlake-hack/pin-mapping-hack.patch

# -> -> <Save> and then <exit>
make menuconfig
make oldconfig
make -j$(nproc)

# ensure no warnings are emitted on make install
curl https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/tree/i915/tgl_huc_7.5.0.bin --output tgl_huc_7.5.0.bin && sudo chmod root:root tgl_huc_7.5.0.bin  && sudo mv /lib/firmware/i915/

# ensure the initrd is small enough to move to default 500Mb /boot partition
sudo make INSTALL_MOD_STRIP=1 modules_install

# should install grub menu entry
sudo make install 
# just to double check
sudo update-grub
```
