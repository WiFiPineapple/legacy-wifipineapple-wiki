# Build Guide

Below is the modified OpenWRT source on which the WiFi Pineapple software is developed. This permits building an OpenWRT image for the MKV hardware as well as cross-compiling binaries for the MIPS architecture used by the Pineapple.

## Prerequisites

In order to build an OpenWRT image which runs on the WiFi Pineapple MKV hardware, or to cross compile packages, there are a few prerequisites required.

First of all, this guide assumes that Ubuntu is used as the host system. If this is not the case for you, then you may need to alter the steps accordingly. The following packages are needed:

```
sudo apt-get install build-essential subversion git-core libncurses5-dev zlib1g-dev gawk flex quilt libssl-dev xsltproc libxml-parser-perl mercurial bzr ecj cvs unzip gcc-multilib gettext
```

**It is also recommended that a [USB 3.3V UART Serial cable](https://hakshop.myshopify.com/collections/accessory/products/serial-ttl-cable) is available as it will most likely be needed when experimenting with firmwares.**

Do **NOT** proceed unless you know what you are doing: Custom firmwares can brick (and even hard brick!) your devices.


## Building OpenWRT for the WiFi Pineapple MKV

The instructions below detail the process of generating firmware images for the WiFi Pineapple MKV hardware. The commands below are all executed in the root of the extracted directory.

### Download and extract the source:

```
wget http://wifipineapple.com/mk5/source.tar.gz
tar -zxvf source.tar.gz
cd ./MK5
```

### Adding software feeds

The commands below will download additional packages that can be built into the firmware.

```
./scripts/feeds update -a
./scripts/feeds install -a
```

### Adding custom files

To add custom files to the build, the `./files/` directory is used. It represents the root of the firmware (i.e /). Creating a folder called "etc" inside of the `./files/` folder and placing a file inside will place (and overwrite) said file in the root filesystem. Care should be taken if you intend to overwrite a file that would otherwise already exist (for example, making incorrect modifications to /etc/config/wireless or /etc/config/wireless could mean that you are unable to connect to your Pineapple via WiFi and/or SSH into it!).

```
mkdir -p ./files/etc/
touch ./files/etc/custom_file
echo "Content" > ./files/etc/custom_file
```

This will create a file called custom_file in the /etc/ folder of the final firmware image.

### Preparing the build
We need to generate a `.config` file which will contain all the details of the packages and kernel modules that will be included in the build.

```
make defconfig
make prereq
```

After executing the above, we can now edit `.config`. It is a terrible idea to attempt to do this manually and thankfully OpenWRT provide a simple way to do it safely. Issue the following command and use the ncurses interface to add/remove anything you wish. It is a good idea to keep any packages that are already selected as they were chosen by the previous commands. 

```
make menuconfig
```

### Compiling the firmware
Once you're happy with the firmware configuration, it is time to build the tools, toolchain, and the firmware image. This will take a (*very*) long time.

```
make
```

After compiling the tools, toolchain, and firmware once, it is possible to build on multiple cores at the same time. **DO NOT DO THIS ON THE FIRST COMPILE**.

```
make -j<number of cores+1>
```

### Installing your firmware on the WiFi Pineapple MKV hardware

Once the firmware has been compiled, it can be located in the `./bin/ar71xx/` folder. There are two relevant files:

```
openwrt-ar71xx-generic-mk5-v1-squashfs-sysupgrade.bin
openwrt-ar71xx-generic-mk5-v1-squashfs-factory.bin
```

The easiest way of installing a new firmware is to boot the WiFi Pineapple MKV and transfer the *-sysupgrade.bin file over to it. This can be done via the SD card or via SSH. Then, the following command can be executed to perform the upgrade.

```
sysupgrade -n /path/to/sysupgrade.bin
```

Should the above not be possible, the second file comes into play. This file can be used in the WiFi Pineapple MKV's recovery interface. [Unbricking a bricked WiFi Pineapple MKV](https://WiFiPineapple.com/?flashing) contains all required instructions.


## Building packages for the WiFi Pineapple MKV
To be able to build packages and/or cross compile them for the WiFi Pineapple's architecture, the above instructions on building a firmware have to be followed first. Please keep in mind, binary files may not be shipped as part of WiFi Pineapple Infusions. See the WiFi Pineapple Infusion forums for more information.

### Example package

To make things simple, the modified source referenced above contains an example package found in ./package/example-package/. This package, especially the two Makefiles contained, contain all the information necessary to build custom packages.

### Compiling the example package
To compile the package, you will now need to go into your build configuration. Make sure you are in the root of the source code directory.

```
make menuconfig
```

Now, navigate to the location of your package. The example package can be found under utilities->example-package. Select it by pressing M. The symbol next the to the package name will change from `< >` to `<M>`. Exit out and save your configuration. Then execute:

```
make package/example-package/compile
```
The built package can now be found in `./bin/ar71xx/packages/example-package_1_ar71xx.ipk`. You can transfer this file and then install it on your WiFi Pineapple using opkg:

```
opkg install example-package_1_ar71xx.ipk
```

### Baking the package into the firmware

Baking a package into the firmware is as simple as repeating the above steps on compiling the package, except that this time, the package needs to be selected differently using the `make menuconfig` command. Instead of selecting it with M, it must be selected with Y. The symbol next the to the package name will change from `< >` to `<*>`. After this is complete, the firmware can be recompiled using the same command as before. This time, the resulting firmware will have the package built in.

```
make
```

## Further Reading

+ http://wiki.openwrt.org/about/toolchain
+ http://wiki.openwrt.org/doc/howto/buildroot.exigence
+ http://wiki.openwrt.org/doc/howto/build
+ http://wiki.openwrt.org/doc/devel/crosscompile
+ http://wiki.openwrt.org/doc/howto/obtain.firmware.sdk
