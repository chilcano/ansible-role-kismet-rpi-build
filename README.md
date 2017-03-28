# Ansible Role: kismet-rpi-build

An Ansible Role that builds / compiles from scratch and packs (Debian/Raspbian binary) [Kismet](http://www.kismetwireless.net) on a Raspberry Pi.
This Role provides the following features:

- Download the Kismet source code.
- Compile the source code in a Raspberry Pi.
- Generate a Kismet Debian/Raspbian package suitable for Raspberry Pi (ARMv7).

## Requirements

- A Raspberry Pi to build/compile from source code.
- The Raspberry Pi connected to your Local LAN.

## Role Variables

Default variables are in `defaults/main.yml` and `vars/main.yml`.

### Variables used to download `src tarball` and `build`.
````
kismet_rpi_build_id: "kismet"
kismet_rpi_build_version: "2016-07-R1"
kismet_rpi_build_version_number: "2016-07"
kismet_rpi_build_version_release: "R1"
kismet_rpi_build_src_ext: "tar.xz"
kismet_rpi_build_src_www_path: "http://www.kismetwireless.net/code"
kismet_rpi_build_architecture: "armhf"
````

### Variables used in `publish`.
```
kismet_rpi_build_publish: true
kismet_rpi_build_localmirror_dir_name_www: "localmirror"
kismet_rpi_build_localmirror_dir_name_local: "/Users/Chilcano/1github-repo/binaries/"
```

### Variables used in `clean`.
```
kismet_rpi_build_clean: false
kismet_rpi_build_remove_dependencies: false
kismet_rpi_build_warpi_start_script: warpi.sh
kismet_rpi_build_warpi_service_name: warpi
kismet_rpi_build_kismet_conf_log: /var/log/kismet
```

## Dependencies

```
$ sudo ansible-galaxy install geerlingguy.apache

$ ansible-galaxy list -vvv

No config file found; using defaults
Opened /Users/Chilcano/.ansible_galaxy
- geerlingguy.apache, 2.0.1
- knopki.locale, a1232f836b5514c58da381d9479640e40d874906
- Stouts.hostname, 1.1.0
- Stouts.timezone, 2.2.0
```

## Example Playbook

Using the Ansible Role in a Raspberry Pi for building/compiling:

```
---
- hosts: pibuilder
  become: yes

  vars_files:
    - vars.yml

  roles:
    - { role: chilcano.kismet-rpi-build }
```

The `inventory` file contains:
```
[pibuilder]
192.168.1.204

[pibuilder:vars]
ansible_ssh_user=picuy
```

## License

MIT / BSD

## Author Information

This role was created in 2017 by Roger Carhuatocto <chilcano@intix.info>, author of [HolisticSecurity.io Blog](https://holisticsecurity.io).
