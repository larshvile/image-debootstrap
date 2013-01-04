image-debootstrap
=================

Creates a bootable image containing a minimal Debian installation + kernel.


Install the base system & kernel to a staging folder
----------------------------------------------------
```bash
sudo ./image-debootstrap install -c config/some-config-file
```
- creates 'work/disk.staging.install.tar', containing the base installation


Customize it
------------
```bash
sudo ./image-debootstrap customize -c config/some-config-file -s path/to/my-customization-scripts [-a my-own-disk.staging.tar]
```
- creates 'work/disk.staging.customize.tar', containing the customized installation

Generate the image
------------------
```bash
sudo ./image-debootstrap bundle -c config/some-config-file [-a my-own-disk.staging.tar]
```
- creates 'work/disk.img', containing a partition table, and a bootable partition with the installation
- qemu-system-$arch work/disk.img launches the image in qemu
- dd if=work/disk.img of=/dev/$someDevice writes the image onto a disk (or use ./write-image-to-device)

