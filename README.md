Mavelous Raspberry Pi Image
=======================

This repositoy will eventaully contain all of the build information for a
Linux image for the Raspberry Pi which will run Mavelous as a server, without
any user intervention. Right now, however, it just builds the vanilla
raspberrypi Yocto build.

This image is built using the Yocto project's Poky tool.
You'll need to clone the Poky trunk in this repository's parent directory:
```  
  $ git clone git://git.yoctoproject.org/poky
```
Then, while still in the `mavelous-rpi-build` parent directory, use the Poky
`oe-init-build-env` tool to setup your shell's environment.
```
  $ source poky/oe-init-build-env `mavelous-rpi-build`
```
Your current directory will be changed to mavelous-rpi-build as part of this
script.

You may then use bitbake to build an image for your Raspberry Pi.
```
  $ bitbake rpi-basic-image
```
The resulting image will be found in `rpi-build/tmp/deploy/images/`.

Use the `dd` tool to write the newly created image to an SD card. Make sure
the SD card's partitions are all unmounted before you begin. On my machine, the SD card is found at `/dev/mmcblk0` - yours may be elsewhere.
```
  $ dd bs=1M if=tmp/deploy/images/rpi-basic-image-raspberrypi.rpi.sdimage of=/dev/mmcblk0
```

You should then be able to insert the card into your raspberry pi and it will
boot, show a splash screen, and then a console. The `root` user will have no
password.

