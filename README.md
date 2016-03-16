# uLinux

**uLinux** (micro/unnamed Linux) is a Buildroot-based Linux distribution targeting IoT gateways**<sup>1</sup>**. Albeit being currently aimed at Raspberry Pis, adaptating it to any other development board is straightforward.

uLinux comes with its own updating infrastructure that enforces security by default. By implementing updates as the download of full filesystem images, their subsequent cryptographically-secure integrity verification and flashing, the system takes into account the constraints of IoT devices while guaranteeing confidentiality, integrity and source authentication of the update image.

## Table of Contents
1. [Design](#design)
2. [Planned features](#planned-features)
3. [Survey](#survey)
4. [License](#license)

### Design

The system is modular and consists of the following components:

#### Update Server

It's responsible for serving update images to devices and keeping track of their statuses. Receives signed update images from the Signing Server. 

#### Signing Server

It's responsible for receiving update images from authenticated developers, generating their cryptographic signatures, packaging and uploading them to the Update Server.

#### Device Daemon

It's responsible for asking for or being notified of new updates, downloading available updates, verifying them and then rebooting the device. The device's init system is then responsible for flashing the new filesystem image on the next boot.

#### Distribution and Development Tools

Buildroot configurations that compile the Kernel, generate the system's initramfs and root filesystem and tools that enable the generation of complete RPi sdcard images and the upload it the root filesystem image to the Signing Server.

### Planned features

- **Automatic Port Forwarding using UPnP**: the Device Daemon becomes responsible for setting up port forwarding to expose its endpoints to the Internet, when behind a NAT.

- **Automated Key Management**: automatically add all required Keys, Certificates and Certificate Authorities to update image, before signing it, by the Signing Server.
 
- **Update Server Dashboard**: create a dashboard accessible by the developers and served by the Update Server that allows users to search for devices and read their statuses (firmware version, IP address, last time online, etc).

- **Device Certificate Regeneration**: as it stands, the system relies on a client certificate to authenticate updating Devices. This feature would allow for the Device to be called by the Update Server to regenerate its certificate using the latest version of its Certificate Authority.

### Survey

We have a working prototype with a lot of missing features and we'd love to hear from you. Is this any good? Would you use it? Which features would you consider top priority? Please helps us out by filling this quick [survey](#link).

### License

This project is [MIT licensed](https://opensource.org/licenses/MIT). That means you're able to use it for your own purposes, whichever they may be, without any cost or obligation.

----
**<sup>1</sup>** - A device that acts as an interface between lesser capable devices (e.g., sensors) and the Internet, translating protocols, doing initial processing of collected data and uploading it to an external API. An IoT gateway may have sensing capabilities in itself.
