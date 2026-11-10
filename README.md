# Android kernel 5.10 for Xiaomi Redmi Note 5 Pro (whyred)

A 5.10 port for whyred, based on the Android Common Kernel
android12-5.10 tree (ramabondanp/android_kernel_common-5.10),
Linux 5.10.272. This is not an upgrade of the 4.19 tree
(anythinganywantanywere/android_kernel_xiaomi_sdm660_419) — that
one is the CAF downstream kernel. This tree starts from ACK and
ports the device over: the device tree is built on sdm630.dtsi,
the mmcc clock driver and the Synaptics TD4310 panel driver are
backported from mainline 7.2, and the config is GKI-style.

Status: it boots to /init, and the display driver comes up
(DRM/MSM with the TD4310 panel — the screen goes dark with the
backlight on once DRM takes over). USB does not enumerate and
adb does not work, and the boot animation never appears. This
is a work in progress, not a daily driver.

Build with NDK r27d clang:

    make O=out-whyred-ack ARCH=arm64 LLVM=1 LLVM_IAS=1 CROSS_COMPILE=aarch64-linux-gnu- LOCALVERSION= -j4 Image.gz qcom/sdm636-xiaomi-whyred.dtb

The defconfig is arch/arm64/configs/whyred_ack_defconfig. To
flash, append the DTB to the kernel (Image.gz-dtb is just
Image.gz plus the DTB concatenated), package it with AnyKernel3,
and flash the zip from Lineage Recovery.

Thanks to ramabondanp for the ACK base, and to Alexey
Minnekhanov and Mathesh Velayudan for the mainline whyred device
tree and the mmcc/panel sources it is based on.
