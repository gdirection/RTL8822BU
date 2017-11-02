# RTL8822BU
Cross-compiling RTL8822BU EDIMAX EW-7822ULC Linux Driver to Raspberry Pi


Follow RPI official kernel build process and install the new kernel image into your Raspberry Pi SD card  
https://www.raspberrypi.org/documentation/linux/kernel/building.md
    
Download driver from Edimax website and unzip
http://www.edimax.com/edimax/download/download/data/edimax/global/download/for_home/wireless_adapters/wireless_adapters_ac1200_dual-band/ew-7822ulc

Go to driver folder
Modified Makefile
  Add a line code
  CONFIG_PLATFORM_ARM_RPI = y
  	
  Add Code snippets
	ifeq ($(CONFIG_PLATFORM_ARM_RPI), y)
	EXTRA_CFLAGS += -DCONFIG_LITTLE_ENDIAN
	ARCH := arm
	CROSS_COMPILE := arm-linux-gnueabihf-
	KVER  := 
	KSRC ?= your raspberry header folder  (ex: /home/john/rp2/linux)
	MODDESTDIR := /lib/modules/$(KVER)/kernel/drivers/net/wireless/
  endif

Make 
It will generate a kernel module 88x2bu.ko, copy this kernel module into your raspberry SD card
	
sudo cp 88x2bu.ko /lib/modules/$(uname -r)/kernel/drivers/net/wireless
depmod -a
modprobe 88x2bu.ko
	
Important !! kernel version of raspberry image should be the same as your build environment and driver module !! 
