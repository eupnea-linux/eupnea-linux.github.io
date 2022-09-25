# Building Eupnea
Due to licensing restraints, Eupnea cannot be distributed as an iso. Instead, it has to be build locally on the device.

## Prerequisites: 
* [A supported Chromebook](/pages/devices)
* A device to build Eupnea on, which can be one of the following:
  * A Chromebook with Crostini enabled(aka "Linux" in settings).
  * A Linux pc/laptop(all distros supported)
  * Windows users will need to [install WSL](https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-10#1-overview).
  * Apple device support is unknown.
  * Android with Termux is not supported
* Developer mode enabled on your chromebook([How to enable developer mode](https://www.androidauthority.com/how-to-enable-developer-mode-on-a-chromebook-906688/))
* A USB-stick or SD-card with 12GB of storage
* IF not using direct write: 10GB of free space on the "builder" device
* Python 3.10 is required for running the `build.py` script

## Instructions:

**If running under crostini(aka "Linux" on ChromeOS)**, follow [these instructions](/pages/crostini.md?id=crostini-specific-instructions) first.
1. Open the terminal, clone the repo and start the script with this command:
    ```
    git clone --depth=1 https://github.com/eupnea-linux/eupnea; cd eupnea; ./build.py
    ```
2. Follow the instructions inside the Terminal.

3. If you chose the image option, flash the image to a USB-stick/SD-card using Etcher, Rufus, DD, or any other tool.
    - If you're running this within Crostini, copy it to a folder you can access from ChromeOS's Files App and then change the `.img` file's extension to `.bin`.
    - You can then [flash](https://www.virtuallypotato.com/burn-an-iso-to-usb-with-the-chromebook-recovery-utility/) it by using the Chrome Recovery Tool.
    
4. [Enable Devloper mode](https://www.androidauthority.com/how-to-enable-developer-mode-on-a-chromebook-906688/) now, if you havent done so yet.

5. Boot into ChromeOS, open the shell by pressing <kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>T</kbd>, enter `shell` and press <kbd>Enter</kbd>.  

6. Inside the chromeos shell enable USB and Custom Kernel Booting by running:
    ```
    sudo crossystem dev_boot_usb=1; sudo crossystem dev_boot_signed_only=0; sync
    ```

7. Reboot with the USB plugged in and press <kbd>CTRL</kbd>+<kbd>U</kbd> or select "External". 

After a short black screen Eupnea should boot.

## Enable Audio
To enable audio on Eunea, follow the instructions below:

1. Boot into Eupnea

2. Make sure you are connected to the internet.

- Skylake, Kaby Lake, or Coffee Lake (7th/8th Gen Intel CPU):
  1. Switch to alt kernel by running: *insert alt switch command here* in the Terminal.
  2. Reboot Eupnea
  3. Run `setup-audio` in the Terminal.
  4. Reboot again
- Apollo Lake(codenames: `CORAL` and `REEF`):
  1. Run: `apl-sof-setup-audio` in the Terminal.
- Everything else: 
  1. Run: `sof-setup-audio` in the Terminal.

If audio still doesn't work, please open an issue with your device codename and generation.

> #### Skylake (SKL) / Kabylake (KBL) disclaimer
>
> If you have a Skylake or Kabylake device, do not change the UCM files (`/usr/share/alsa/ucm2/`) in an attempt to use PulseAudio. If you have no idea what any of these are, you can safely ignore this.
>
> PulseAudio, without UCM modifications, errors out. If you modify the UCM to remove the `Front Mic`, `Rear Mic`, and `Mic` (all of these are related to PCM3 on `da7219max`), PulseAudio and general audio will work, but your speakers **will be fried** or their membranes **will burst**.

## Optional:
#### ZRAM(aka swap in ram):
The commands below will create 6GB of memory compressed to 2GB.  
To enable "extra" memory run the following commands in the terminal:  
1. ``sudo modprobe zram``
2. ``SIZE=6144 # change the size here if you want more/less swap memory``
3. ``sudo echo $(($SIZE*1024*1024)) > /sys/block/zram0/disksize``
4. ``sudo mkswap /dev/zram0``
5. ``sudo swapon /dev/zram0 -p 10``  

#### Fan Control/ectool:
To install the chromeos ectool utility run: ``install-ectool``

#### Installing to Internal Storage

This will wipe ChromeOS(or any other currently installed OS). It is always possible to [restore ChromeOS using a recovery USB](https://support.google.com/chromebook/answer/1080595?hl=en). It's recommended to [setup audio](?id=enable-audio) and confirm all hardware is working correctly(touchpad, touchscreen, speakers).

1. ~~Find your internal storage disk by running `lsblk`. Chances are this will be `/dev/mmcblk0` or similar. Keep this device name in mind.
   If you are unable to find your internal storage, run `mount | sed -n 's|^/dev/\(.*\) on / .*|\1|p'` within the ChromeOS Terminal. The ChromeOS Terminal is accessed by typing in CTRL + ALT + T and entering in `shell`~~
2. ~~Open a terminal and run `install-to-internal-storage` on your Chromebook with the Breath USB booted.~~

*Insert better instructions here*
