---
layout: base
title: Interfaces reference
---

[Interfaces documentation](/core/interfaces)

## Terminology

* Auto-connect: the interface is connected upon snap install

* Transitional: the interface supports traditional desktop features that were not designed with strong application isolation in mind and will be deprecated when a technology more in adequacy with the snap security policy is available.

## Interfaces

| Interface name | Auto-connect | Transitional | Attributes |
|----------------|--------------|--------------|------------|
| `account-control` | no | no |  |
| `alsa` | no | no |  |
| `autopilot-introspection` | no | no |  |
| `avahi-control` | no | no |  |
| `avahi-observe` | no | no |  |
| `bluetooth-control` | no | no |  |
| `bluez` | no | no |  |
| `broadcom-asic-control` | no | no |  |
| `browser-support` | no when <br/>`allow-sandbox: true`, <br/>yes otherwise | no | `allow-sandbox:` true or false<br/>(defaults to ``false``) |
| `camera` | no | no |  |
| `classic-support` | no | no |  |
| `content` | yes for snaps from same publisher, no otherwise | no | `read` (slot)<br/> `write` (slot)<br/>  `content` (slot)<br/> `default-provider` (plug)<br/> `target` (plug)<br/> `content` (plug) |
| `core-support` | no | no |  |
| `cups-control` | no | no |  |
| `dbus` | no | no | `name` (slot)<br/> `bus` (slot)<br/> `name` (plug)<br/> `bus` (plug) |
| `dcdbas-control` | no | no |  |
| `desktop-legacy` | yes | yes |  |
| `desktop` | yes | no |  |
| `docker-support` | no | no | `privileged-containers` (plug): true or false <br/>(defaults to ``false``) |
| `docker` | no | no |  |
| `firewall-control` | no | no |  |
| `framebuffer` | no | no |  |
| `fuse-support` | no | no |  |
| `fwupd` | no | no |  |
| `gpio-memory-control` | no | no |  |
| `gpio` | no | no |  |
| `greengrass-support` | no | no |  |
| `gsettings` | yes | yes |  |
| `hardware-observe` | no | no |  |
| `hardware-random-control` | no | no |  |
| `hardware-random-observe` | no | no |  |
| `hidraw` | no | no |  |
| `home` | yes on classic <br/>(traditional distributions), <br/>no otherwise | yes |  |
| `i2c` | no | no |  |
| `iio` | no | no |  |
| `io-ports-control` | no | no |  |
| `joystick` | no | no |  |
| `kernel-module-control` | no | no |  |
| `kubernetes-support` | no | no |  |
| `kvm` | no | no |  |
| `libvirt` | no | no |  |
| `locale-control` | no | no |  |
| `location-control` | no | no |  |
| `location-observe` | no | no |  |
| `log-observe` | no | no |  |
| `lxd-support` | no | yes |  |
| `lxd` | no | no |  |
| `maliit` | no | no |  |
| `media-hub` | yes | no |  |
| `mir` | yes | no |  |
| `modem-manager` | no | no |  |
| `mount-observe` | no | no |  |
| `mpris` | no | no | `name` (slot) |
| `netlink-audit` | no | no |  |
| `netlink-connector` | no | no |  |
| `network-bind` | yes | no |  |
| `network-control` | no | no |  |
| `network-manager` | no | no |  |
| `network-observe` | no | no |  |
| `network-setup-control` | no | no |  |
| `network-setup-observe` | no | no |  |
| `network-status` | yes | no |  |
| `network` | yes | no |  |
| `ofono` | no | no |  |
| `online-accounts-service` | yes | no |  |
| `opengl` | yes | no |  |
| `openvswitch-support` | no | no |  |
| `openvswitch` | no | no |  |
| `optical-drive` | yes | no |  |
| `password-manager-service` | no | yes |  |
| `physical-memory-control` | no | no |  |
| `physical-memory-observe` | no | no |  |
| `ppp` | no | no |  |
| `process-control` | no | no |  |
| `pulseaudio` | yes | no |  |
| `raw-usb` | no | no |  |
| `removable-media` | no | no |  |
| `screen-inhibit-control` | yes | no |  |
| `serial-port` | no | no |  |
| `shutdown` | no | no |  |
| `snapd-control` | no | no |  |
| `spi` | no | no |  |
| `storage-framework-service` | no | no |  |
| `system-observe` | no | no |  |
| `system-trace` | no | no |  |
| `thumbnailer-service` | no | no |  |
| `time-control` | no | no |  |
| `timeserver-control` | no | no |  |
| `timezone-control` | no | no |  |
| `tpm` | no | no |  |
| `ubuntu-download-manager` | yes | no |  |
| `udisks2` | no | no |  |
| `uhid` | no | no |  |
| `unity7` | yes | yes |  |
| `unity8-calendar` | no | no |  |
| `unity8-contacts` | no | no |  |
| `unity8` | yes | no |  |
| `upower-observe` | yes | no |  |
| `wayland` | yes | no |  |
| `x11` | yes | yes |  |

*  account-control : Can create and delete non-system extra users and change the password for non-system extra users (_2.22+_). 
*  alsa : Can directly access ALSA devices in /dev/snd.
*  autopilot-introspection : Can be introspected by autopilot (_2.24+_).
* `avahi-control`: Can access and control snaps providing Avahi mDNS/DNS-SD services on the network which gives privileged access to the service (_2.28+_).
* `avahi-observe`: Can access snaps providing Avahi to browse for mDNS/DNS-SD services on the network.
* `bluetooth-control`: Allow to manage the kernel side Bluetooth stack.
* `bluez`: Can access snaps providing the bluez interface which gives privileged access to bluetooth.
* `broadcom-asic-control`: Can access broadcom-asic devices and sysfs interfaces (_2.28+_).
* `browser-support`: Can access files and IPC needed by modern browsers. This interface is intended to be used when using an embedded Chromium Content API or using the sandboxes in major browsers from vendors like Google and Mozilla. The `allow-sandbox` attribute may be used to give the necessary access to use the browser\'s sandbox functionality.
* `camera`: Can access the first video camera. Suitable for programs wanting to use webcams.
* `classic-support`: Allows resources necessary for running as classic dimension snap which gives device ownership to the snap. This interface is reserved for the `classic` snap (_2.23_).
* `content`: Can access content from the providing snap from within the consuming snap\'s filesystem area.
    * `read` (slot): read-only paths from providing snap to expose to the consuming snap.
    * `write` (slot): read-write paths from providing snap to expose to the consuming snap.
    * `content` (slot): reference to plug side of connection. Defaults to local slot name.
    * `default-provider` (plug): name and slot of preferred providing snap (`<SNAP>:<SLOT>`).
    * `target` (plug): path in consuming snap to find providing snap\'s files.
    * `content` (plug): reference to slot side of connection. Defaults to local plug name.
* `core-support`: Can control all aspects of systemd via the systemctl command, update rsyslog configuration, update systemd-timesyncd configuration and update/apply sysctl configuration which gives privileged access to the system (_2.22+_). Reserved for `core` snaps (`type: os`).
* `cups-control`: Can access cups control socket which gives privileged access to configure printing.
* `dbus`: Providing snaps implementing a DBus API may be accessed via their well-known DBus connection name (_2.20+_).
    * `name` (slot): well-known DBus connection name for the service (eg, `org.foo.bar`).
    * `bus` (slot): DBus bus to use (ie, `session` or `system`).
    * `name` (plug): well-known DBus connection name of the service from the providing snap.
    * `bus` (plug): DBus bus to use for providing snap
* `dcdbas-control`: Can interact with the Dell Systems Management Base Driver which provides a sysfs interface for systems management software such as Dell OpenManage to perform system management interrupts and host control actions (system power cycle or power off after OS shutdown) on certain Dell systems.
* `desktop-legacy`: Can access desktop legacy methods such as a11y and input methods which gives privileged access to sensitive information and does not prevent eavesdropping or apps interfering with each other (_2.28+_).
* `desktop`: Can access basic desktop graphical resources (_2.28+_). This interface is designed to be used with other interfaces, such as wayland.
* `docker-support`: Can access resources and syscalls necessary to run Docker application containers. The `privileged-containers` attribute may be used to give the necessary access to run privileged containers. Providing snaps specifying this interface currently may only be established with the Docker project.
    * `privileged-containers` (plug): true or false (defaults to ``false``)
* `docker`: Can access snaps providing the docker interface which gives privileged access to the system.
* `firewall-control`: Can configure network firewalling giving privileged access to networking.
* `framebuffer`: Can use the universal framebuffer (/dev/fb[0-9]*, (_2.22+_)).
* `fuse-support`: Can mount fuse filesystems (as root only).
* `fwupd`: Can access snaps providing the fwupd interface which gives privileged access to update UEFI capsule format firmware.
* `gpio-memory-control`: Can access all GPIO memory via /dev/gpiomem. This is restricted because it provides privileged access to all GPIO devices (_2.30+_).
* `gpio`: Can access GPIO devices. This is restricted because it provides privileged access to GPIO hardware.
* `greengrass-support`: Can access resources and syscalls necessary to run Amazon Greengrass services and lambda functions. Providing snaps specifying this interface currently may only be established with the Amazon Greengrass project  (_2.26+_).
* `gsettings`: Can access global gsettings of the user\'s session which gives privileged access to sensitive information stored in gsettings and allows adjusting settings of other applications.
* `hardware-observe`: Can query hardware information from the system.
* `hardware-random-control`: Allow read/write access to `/dev/hwrng` (_2.25+_).
* `hardware-random-observe`: Allow read access to `/dev/hwrng` (_2.25+_).
* `hidraw`: Can access hidraw devices. This is restricted because it provides privileged access to hardware devices.
* `home`: Can access non-hidden files in user\'s `$HOME` and gvfs mounted directories owned by the user to read/write/lock.
* `i2c`: Can access i2c devices. This is restricted because it provides privileged access to hardware devices.
* `iio`: Can access IIO devices. This is restricted because it provides privileged access to IIO hardware (_2.20+_).
* `io-ports-control`: Can write to `/dev/port` to change the I/O port permissions and privilege level of the calling process and disable interrupts (_2.21+_).
* `joystick`: Can access `/dev/js*` devices (_2.24+_).
* `kernel-module-control`: Can insert kernel modules. This interface gives privileged access to the device.
* `kubernetes-support`: Can access resources and syscalls necessary to operate as the Kubernetes service and run application containers (_2.25+_).
* `kvm`: Can access `/dev/kvm` which gives privileged access to the kvm hypervisor (_2.28+_).
* `libvirt`: Can access the libvirt control socket, which gives privileged access to control libvirtd on the host. This is commonly used to create and manage QEMU/KVM instances on the host.
* `locale-control`: Can manage locales directly separate from `config core`.
* `location-control`: Can access snaps providing the location-control interface which gives privileged access to configure, observe and use location services.
* `location-observe`: Can access snaps providing the location-observe interface which gives privileged access to query location services.
* `log-observe`: Can read system logs and set kernel log rate-limiting.
* `lxd-support`: Can access all resources and syscalls on the device for LXD to mediate access for its containers. This interface currently may only be established with the upstream LXD project.
* `lxd`: Can use the LXD API via the socket provided by the "lxd" snap. LXD_DIR must be set to /var/snap/lxd/common/lxd. This interface requires manual connection.
* `maliit`: Can access snaps providing the maliit input interface (_2.24+_).
* `media-hub`: Can access snaps providing the media-hub interface (_2.25+_).
* `mir`: Can access snaps providing the mir display server interface.
* `modem-manager`: Can access snaps providing the modem-manager interface which gives privileged access to configure, observe and use modems.
* `mount-observe`: Can query system mount information. This is restricted because it gives privileged read access to mount arguments and should only be used with trusted apps.
* `mpris`: Providing snaps implementing the Media Player Remote Interfacing Specification (mpris) may be accessed via their well-known DBus name.
    * `name` (slot): optional, media player name to use for DBus well-known name.
* `netlink-audit`: Can communicate via NETLINK_AUDIT (_2.26+_).
* `netlink-connector`: Can communicate via NETLINK_CONNECTOR (_2.26+_).
* `network-bind`: Can access the network as a server.
* `network-control`: Can configure networking and network namespaces via `ip netns` (_2.20+_) which gives wide, privileged access to networking.
* `network-manager`: Can access snaps providing the network-manager interface which gives privileged access to configure and observe networking.
* `network-observe`: Can query network status information which gives privileged read-only access to networking information.
* `network-setup-control`: Can read/write network setup configuration files. This is restricted because it gives access to system network configuration which can container network security details (_2.22+_).
* `network-setup-observe`: Can read network setup configuration files. This is restricted because it gives access to system network configuration which can contain network security details.
* `network-status`: Can access snaps providing the NetworkingStatus interface (_2.25+_).
* `network`: Can access the network as a client.
* `ofono`: Can access snaps providing the ofono interface which gives privileged access to configure, observe and use ofono devices.
* `online-accounts-service`: Can access snaps providing the Online Accounts Service interface (_2.25+_).
* `opengl`: Can access OpenGL hardware.
* `openvswitch-support`: Enables kernel support for openvswitch (_2.20+_).
* `openvswitch`: Can access the openvswitch control socket, which gives privileged access to control openvswitch on the host (_2.20+_).
* `optical-drive`: Can access the first optical drive in read-only mode. Suitable for CD/DVD playback.
* `password-manager-service`: Can access global password manager services provided by popular Desktop Environment (eg, Secret Service and KWallets) which gives privileged access to sensitive information stored in the user\'s session (_2.27+_).
* `physical-memory-control`: Can write to /dev/mem to access architecture-specific subset of the physical address space for common use cases (eg, X without KMS, dosbox, etc) when kernels are compiled with STRICT_DEVMEM=y (required for certified kernels). With STRICT_DEVMEM=n, can write to all physical memory (_2.21+_).
* `physical-memory-observe`: Can read from /dev/mem to access architecture-specific subset of the physical address space for common use cases (eg, X without KMS, dosbox, etc) when kernels are compiled with STRICT_DEVMEM=y (required for certified kernels). With STRICT_DEVMEM=n, can read from all physical memory (_2.21+_).
* `ppp`: Can access Point-to-Point protocol daemon which gives privileged access to configure and observe PPP networking.
* `process-control`: Can manage processes via signals and nice.
* `pulseaudio`: Can access the PulseAudio sound server which allows for sound playback in games and media application. Recording not supported but will be in a future release.
* `raw-usb`: Can directly access connected USB devices via a raw interface (_2.18+_).
* `removable-media`: Can access files from removable media in /media and /run/media.
* `screen-inhibit-control`: Can access desktop session manager screen inhibit and uninhibit functionality.
* `serial-port`: Can access serial ports. This is restricted because it provides privileged access to configure serial port hardware. Note that the slot is meant to be implemented by a gadget snap (this is not provided by the core snap).
* `shutdown`: Can control the system power state and rebooting, powering off or halting the system.
* `snapd-control`: Can manage snaps via snapd.
* `spi`: Can access SPI devices. This is restricted because it provides privileged access to SPI hardware (_2.28+_).
* `storage-framework-service`: Can access snaps providing the Storage Framework Service interface (_2.25+_).
* `system-observe`: Can query system status information which gives privileged read access to all processes on the system.
* `system-trace`: Can use kernel tracing facilities. This is restricted because it gives privileged access to all processes on the system and should only be used with trusted apps.
* `thumbnailer-service`: Can access snaps providing the thumbnailer service interface (_2.22+_).
* `time-control`: Can set system time and date and query systemd-timedated for time information.
* `timeserver-control`: Can manage timeservers via systemd-timedated and directly separate from `config core`.
* `timezone-control`: Can manage timezone via systemd-timedated and directly separate from `config core`.
* `tpm`: Can access the tpm device /dev/tpm0.
* `ubuntu-download-manager`: Can access snaps providing the ubuntu-download-manager interface.
* `udisks2`: Can access snaps providing the udisks2 interface which gives privileged access to storage on the device.
* `uhid`: Can access /dev/uhid to create kernel hid devices from user-space which gives privileged access to HID transport drivers.
* `time-control`: Can set system time and date and query systemd-timedated for time information.
* `timeserver-control`: Can manage timeservers via systemd-timedated and directly separate from `config core`.
* `timezone-control`: Can manage timezone via systemd-timedated and directly separate from `config core`.
* `tpm`: Can access the tpm device /dev/tpm0.
* `ubuntu-download-manager`: Can access snaps providing the ubuntu-download-manager interface.
* `udisks2`: Can access snaps providing the udisks2 interface which gives privileged access to storage on the device.
* `uhid`: Can access /dev/uhid to create kernel hid devices from user-space which gives privileged access to HID transport drivers.
* `unity7`: Can access Unity7. Unity 7 runs on X and requires access to various DBus services. This interface grants privileged access to the user\'s session since the Unity 7 environment does not prevent eavesdropping or apps interfering with one another.
* `unity8-calendar`: Can access snaps providing the Unity8 calendar interface which gives access to the Unity8 global calendar.
* `unity8-contacts`: Can access snaps providing the Unity8 contacts interface which gives access to the Unity8 global contacts list.
* `unity8`: Can access Unity8 (_2.22+_). This interface is in active development and should not yet be used in production and its use is therefore restricted.
* `upower-observe`: Can access snaps providing the UPower interface for power devices, history and statistics.
* `wayland`: Can access compositors supporting the wayland protocol  (_2.28+_).
* `x11`: Can access the X server which gives privileged access to the user\'s session since X does not prevent eavesdropping or apps interfering with one another.