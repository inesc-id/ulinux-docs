# uLinux

uLinux (micro/unnamed Linux) is a Buildroot-based Linux distribution targeting IoT gateways. Albeit being currently aimed at Raspberry Pis, adaptating it to any other development board is straightforward.

uLinux comes with its own updating infrastructure that enforces security by default. By implementing updates as the download of full filesystem images, their subsequent cryptographically-secure integrity verification and flashing, the system takes into account the constraints of IoT devices while guaranteeing confidentiality, integrity and source authentication of the update image.

## Table of Contents
1. [Design](#design)

### Design

The system is modular and consists of the following components:

- Update Server

It's responsible for serving update images to devices and keeping track of their statuses. Receives signed update images from the Signing Server. 

- Signing Server

It's responsible for receiving update images from authenticated developers, generating their cryptographic signatures, packaging and uploading them to the Update Server.

- Device Daemon

It's responsible for asking for or being notified of new updates, downloading available updates, verifying them and then rebooting the device. The device's init system is then responsible for flashing the new filesystem image on the next boot.

- Distribution and Development Tools

Buildroot configurations that compile the Kernel, generate the system's initramfs and root filesystem and tools that enable the generation of complete RPi sdcard images and the upload it the root filesystem image to the Signing Server.
