# arv7519rw22-openwrt-pkgs

```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@                                                                                                   @
@   I M P O R T A N T :   P L E A S E   R E A D   B E F O R E   U S I N G   T H E S E   F I L E S   @
@                                                                                                   @
@   DISCLAIMER: These packages are only public because GitHub is convenient for file hosting. Our   @
@               OpenWRT repository wasn't clean when we built these images, so the kernel version   @
@               differs from that of official releases. The idea is to setup opkg to use packages   @
@               from this Git repository instead of using the official OpenWRT releases. At least   @
@               U-boot and the base OpenWRT image work, and it's likely that other things work as   @
@               well. However, this is NOT an official OpenWRT build, so use it at your own risk!   @
@                                                                                                   @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
```

This repository contains OpenWRT packages for the Orange Livebox 2.1
router, also known as Astoria/Arcadyan ARV7519RW22. Newer OpenWRT
releases have disabled support for this device because U-boot fails to
load the larger kernel+initramfs images. In order to make it work, one
needs to add support to build U-boot for this device.

See https://github.com/openwrt/openwrt/pull/9742 and
https://github.com/openwrt/openwrt/pull/9746 for the relevant PRs.

## How to use

First of all, scroll back up and re-read the giant ASCII-framed warning
at the start of this document. The files that were tested can be useful
as reference (they worked for us, and should work for you as well), but
it would be best to not depend on these packages. It should be possible
to use the official packages if one manages to build an OpenWRT release
for the ARV7519RW22 that uses the same kernel version.

0. Read through all these steps before doing anything to your router.
   You will need to set up the UART console as well as a TFTP server.
1. Follow https://openwrt.org/toh/arcadyan/arv7519rw22 to install
   OpenWRT, if you haven't done so already. Make sure U-boot shows up.
   If you want, you can skip flashing the old OpenWRT / LEDE version.
2. Grab `u-boot.bin` (U-boot for ARV7519RW22, NOR version) and flash it
   using `tftpboot u-boot.bin` and `run write-uboot-nor`, then reboot.
   If all goes well, your router is now using a working U-boot version.
3. If the old OpenWRT version does **NOT** work, boot the recovery image
   with `tftpboot openwrt-initramfs-kernel.bin` and `bootm`. If U-boot
   says `LZMA: uncompress or overwrite error 7 - must RESET b` and the
   board immediately resets, you're still using a buggy U-boot version.
4. Once you've managed to boot some OpenWRT version (from NOR or RAM),
   you can simply flash `openwrt-squashfs-sysupgrade.bin` as you would
   do in any other case. LUCI (the web UI) is enabled in our images.
5. If the PRs fixing the ARV7519RW22 haven't been merged yet, consider
   ways to raise awareness of this issue and the availability of a fix,
   such as commenting on the PRs linked above, as well as and asking in
   [OpenWRT's communication channels](https://openwrt.org/contact). It
   goes without saying that you should be civil and look for solutions.
