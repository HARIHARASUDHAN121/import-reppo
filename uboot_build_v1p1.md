# Steps to build U-Boot for Raspberry Pi 3

## 1. Know the RPi3 Architecture

Run the following command on the target (_RPi3_) or Google it.

```shell
uname -m
```

Note this and it'll be used for selecting the `Cross Compiler` in next step

## 2. Download & Set Cross Compiler

1. Head to [arm Developer/Tools and Software/Open Source Software/Developer Tools/GNU Toolchain/GNU Toolchain for the A-profile Architecture/Downloads](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-a/downloads)
2. Select **x86_64 Linux hosted cross compilers** and **AArch64 GNU/Linux target (aarch64-none-linux-gnu)**
   Download the `gcc-arm-10.3-2021.07-x86_64-aarch64-none-linux-gnu.tar.xz`
3. Decompress the downloaded file

```shell
mkdir -p ~/tools
tar -xvf ~/Downloads/gcc-arm-10.3-2021.07-x86_64-aarch64-none-linux-gnu.tar.xz -C ~/tools/
```

4. Export & check the toolchain

```shell
gcc --version
export CC=~/tools/gcc-arm-10.3-2021.07-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu
$CC-gcc --version
```

Note the difference in `host` and `target` GCC

## 3. Download upstream U-Boot source

```shell
git clone https://github.com/u-boot/u-boot.git
cd u-boot
```

## 4. Configure for RPi3

Install the dependencies as required:

```shell
sudo apt install bison flex -y
```

Use `rpi_3_defconfig` for the Raspberry Pi 3

```shell
make -j$(nproc) CROSS_COMPILE=$CC- rpi_3_defconfig
```

## 5. Tweak Configuration

Modify the `Shell prompt` on U-Boot to have your name for learning purposes. Study what is `Shell prompt`

Info can be found here: https://www.denx.de/wiki/DULG/UBootCommandLineInterface

Install the dependencies as required:

```shell
sudo apt install libncurses-dev -y
```

The following command will open a

```shell
make -j$(nproc) CROSS_COMPILE=$CC- menuconfig
```

## 6. Build

Install the dependencies as required:

```shell
sudo apt install libssl-dev -y
```

Build command

```shell
make -j$(nproc) CROSS_COMPILE=$CC- all
```

Analyse the build result

```shell
ll -tr
```

`u-boot.bin` should be the result of the build process

## Reference

- https://github.com/joholl/rpi4-uboot-tpm#building-u-boot
