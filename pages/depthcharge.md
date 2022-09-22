# Depthcharge

Depthcharge is a [U-boot](https://www.denx.de/wiki/U-Boot) based bootloader for Chromebooks. Depthcharge is not a BIOS, nor is it ever meant to be accessed by the end user. As a result, Depthcharge is basically an embedded-systems bootloader.

* No `initramfs` support
    * Makes the Linux boot flow much simpler

Depthcharge supports Multiboot and ZBI (initramfs support for Fuschia on the Pixelbook Pro). This means that, theoretically, you could boot any Multiboot-spec image, like GRUB2.

However, this requires a recompile of the firmware and you ultimately need to disable Write Protect to flash your new firmware. At that point, a better idea would be to [flash UEFI using MrChromebox's script](https://mrchromebox.tech/#fwscript)
