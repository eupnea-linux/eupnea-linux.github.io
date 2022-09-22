# Linux Distributions

You could rip out a `rootfs` from a Linux distro's desktop ISO by extracting a `SquashFS`, but these are not up-to-date, flexible, or uniform. Additionally, they are hardcoded to work with an `initramfs` and have incompatible installers baked-in.

Therefore, Eupnea uses minimal cloud root file systems (meant for Docker, etc.). These require minimal postinstall steps.
