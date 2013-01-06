image-debootstrap
=================

Creates a bootable image containing a minimal Debian installation + kernel.


Install the base system & kernel to a staging folder
----------------------------------------------------
```bash
sudo ./image-debootstrap install -c path-to-some-config-file
```
- creates 'work/disk.staging.install.tar', containing the base installation


Customize it
------------
```bash
sudo ./image-debootstrap customize -c path-to-some-config-file -s path/to/my-customization-scripts [-a my-own-disk.staging.tar]
```
- creates 'work/disk.staging.customize.tar', containing the customized installation

Generate the image
------------------
```bash
sudo ./image-debootstrap bundle -c path-to-some-config-file [-a my-own-disk.staging.tar]
```
- creates 'work/disk.img', containing a partition table, and a bootable partition with the installation
- qemu-system-$arch work/disk.img launches the image in qemu
- dd if=work/disk.img of=/dev/$someDevice writes the image onto a disk (or use ./write-image-to-device)

Configuration file example
--------------------------
```bash
img_size_bytes=$((512 * 1024 * 1024)) # 512MiB

arch=i386
dist=squeeze
kernel_package=linux-image-686

extra_packages="first,second,..."

root_pwd=my-password
hostname=my-hostname

#serial_console=ttyS0
#serial_console_baud=19200
#flash_drive=true

#dhcp_interfaces="eth0 eth1 ..."
#ping_broadcast_reply=true

#ssh_host_rsa_key_path=path-to-custom-host-key
#ssh_authorized_keys+=("my-pub-key")
```

