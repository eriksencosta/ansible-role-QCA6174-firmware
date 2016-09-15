# Ansible role: QCA6174 firmware installation

[![Build Status](https://travis-ci.org/eriksencosta/ansible-role-QCA6174-firmware.svg?branch=master)](https://travis-ci.org/eriksencosta/ansible-role-QCA6174-firmware)

An Ansible role for the installation of the working firmware binaries for the Qualcomm QCA6147 wireless card, which
ships in a lot of recent laptop models.

Running this role should make the WiFi and Bluetooth to function properly.

To check if your laptop comes with this wireless card, use the `lspci` utility command:

    $ sudo update-pciids
    $ lspci | grep QCA6174
    02:00.0 Network controller: Qualcomm Atheros QCA6174 802.11ac Wireless Network Adapter (rev 32)

This setup was tested in a Dell Inspiron 5557 model (Serie 5000 Special Edition, as sold in the Brazilian market,
[Dell specifications][#dell-5557-specs]). As this laptop is a Skylake one (it comes with the 6th generation Intel i7),
using a recent Linux kernel is a better choice because of the better support for the architecture (specially the
[power management][#kernel-skylake-support]).

Installing Debian Stretch (using the [netinstall image with non-free firmware][#stretch-nonfree]) in this laptop made
it to work nicely. The battery have decent life, and the sound, the built-in camera, WiFi and Bluetooth works. The only
exception is the NVIDIA discrete GPU card (the laptop is Optimus-based, with an integrated Intel graphics card and a
NVIDIA GeForce GPU card), so it seems [Linus middle finger][#linus-nvidia] wasn't enough.


## Requirements

- Debian Stretch
- Ansible 2.0


## Role Variables

`qcaf_debian_repository_mirror`: the Debian repository mirror to use. Defaults to `http://httpredir.debian.org/debian`.

As this role installs non-free packages (namely, `firmware-linux`, `firmware-linux-free`, `firmware-linux-nonfree` and
`firmware-atheros`), the `/etc/apt/sources.list` file is manipulated (it backups the original file before).


## Dependencies

None.


## Example Playbook

    - hosts: localhost
      roles:
        - eriksencosta.qca6147-firmware


## License

Apache License 2.0


## Author Information

[Eriksen Costa][#author]


[#dell-5557-specs]: http://downloads.dell.com/manuals/all-products/esuprt_laptop/esuprt_inspiron_laptop/inspiron-15-5557-laptop_reference%20guide_en-us.pdf
[#kernel-skylake-support]: https://mjg59.dreamwidth.org/41713.html
[#stretch-nonfree]: http://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/stretch_di_alpha7/amd64/iso-cd/
[#linus-nvidia]: https://www.youtube.com/watch?v=iYWzMvlj2RQ
[#author]: http://blog.eriksen.com.br
