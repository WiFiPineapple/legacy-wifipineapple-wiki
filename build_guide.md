# Build Guide

Below is the modified OpenWRT source on which the WiFi Pineapple software is developed. This permits building an OpenWRT image for the MKV hardware as well as cross-compile binaries architecture compatible binaries for the system.

## Prerequisites

Building an OpenWRT image which runs on the WiFi Pineapple MKV hardware, or to cross compile packages for the WiFi Pineapple MKV, there are a few prerequisites required.

First of all, this guide assumes that Ubuntu is used as the host system. The following packages are needed:

```
sudo apt-get install build-essential subversion git-core libncurses5-dev zlib1g-dev gawk flex quilt libssl-dev xsltproc libxml-parser-perl mercurial bzr ecj cvs unzip gcc-multilib gettext
```

**It is also recommended that a [USB 3.3V UART Serial cable](https://hakshop.myshopify.com/collections/accessory/products/serial-ttl-cable) is available as it will most likely be needed when experimenting with firmwares.

Do **NOT** proceed unless you know what you are doing: Custom firmwares can brick (and even hard brick) your devices.


## Building OpenWRT for the WiFi Pineapple MKV

The instructions below detail the process of generating firmware images for the WiFi Pineapple MKV hardware. The commands below are all executed in the root of the extracted directory.

### Download and extract source

```
wget http://wiki.wifipineapple.com/uploads/source.tar.gz
tar -zxvf source.tar.gz
cd ./MK5
```

### Adding software feeds

The commands below will allow for additional packages to be built into the firmware.

```
./scripts/feeds update -a
./scripts/feeds install -a
```

### Adding custom files

To add custom files to the build, the `./files/` directory is used. It represents the root of the firmware. Creating a folder called "etc" inside of the `./files/` folder and placing a file inside will place (and overwrite) said file in the firwmare.

```
mkdir -p ./files/etc/
touch ./files/etc/custom_file
echo "Content" > ./files/etc/custom_file
```

The above will create a file called custom_file in the /etc/ folder of the final firmware image.

### Preparing the build

```
make defconfig
make prereq
```

After following the above instructions, execute the command below. This allows the configuration of the firmware build to include / exclude any packages and kernel modules in your build. Once done, the configuration should be saved.

```
make menuconfig
```

### Compiling the firmware
Once happy with the firmware configuration, execute the below command. This will build the tools, toolchain, and firmware image. This will take a long time.

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

The easiest way of installing a firmware is to boot the WiFi Pineapple MKV and transfer the *-sysupgrade.bin file over to it. This can be done via the SD card or via SSH. Then, the following command can be executed to perform the upgrade.

```
sysupgrade -n /path/to/sysupgrade.bin
```

Should the above not be possible, the second file comes into play. This file can be used in the WiFi Pineapple MKV's recovery interface. https://WiFiPineapple.com/?flashing (Unbricking a bricked WiFi Pineapple MKV) contains all required instructions.


## Building packages for the WiFi Pineapple MKV

To be able to build packages and / or cross compile them for the WiFi Pineapple MKV firmware, the above instructions on building a firmware have to be followed first. Please keep in mind, binary files may not be shipped as part of WiFi Pineapple Infusions. See the WiFi Pineapple Infusion forums for more information.

### Example package

To make things simple, the modified source referenced above contains an example package found in ./package/example-package/. This package, especially the two Makefiles contained, contain all the information necessary to build custom packages.

### Compiling the example package
To compile the package, you will now need to go into your build configuration. Make sure you are in the root of the source code directory.

```
make menuconfig
```

Now, navigate to the location of your package. The example package can be found under utilities->example-package. Select it by pressing M. Exit out and save your configuration. Then execute:

```
make package/example-package/compile
```

The built package can now be found in `./bin/ar71xx/packages/example-package_1_ar71xx.ipk`. You can transfer and install this file on your WiFi Pineapple using opkg.

### Baking the package into the firmware

Baking a package into the firmware is as simple as repeating the above steps on compiling the package, except that this time, the package needs to be selected differently using the `make menuconfig` command. Instead of selecting it with M, it must be selected with Y. After this is complete, the firmware can be recompiled using the following commmand. This time, the resulting firmware will have the package built in.

```
make
```

## Further Reading

+ http://wiki.openwrt.org/about/toolchain
+ http://wiki.openwrt.org/doc/howto/buildroot.exigence
+ http://wiki.openwrt.org/doc/howto/build
+ http://wiki.openwrt.org/doc/devel/crosscompile
+ http://wiki.openwrt.org/doc/howto/obtain.firmware.sdk
