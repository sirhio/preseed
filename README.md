#cloud-config
autoinstall:
  apt:
    disable_components: []
    geoip: true
    preserve_sources_list: false
    primary:
    - arches:
      - amd64
      - i386
      uri: http://us.archive.ubuntu.com/ubuntu
    - arches:
      - default
      uri: http://ports.ubuntu.com/ubuntu-ports
  drivers:
    install: false
  identity:
    hostname: wol
    password: $6$QnXm9M7UOitBqiCI$afG8Xs3sE/Z08pBwkrSNoFxkupdOU.ASMIhQQpYIrea3KFmZA0hKTHR9.h3RJwkxUchWWQ6MUO43.9PLE9DQW0
    realname: itrevel
    username: itrevel
  kernel:
    package: linux-generic
  keyboard:
    layout: us
    toggle: null
    variant: ''
  locale: en_US.UTF-8
  network:
    ethernets:
      enp0s3:
        dhcp4: true
    version: 2
  snaps:
  - channel: stable
    classic: false
    name: docker
  source:
    id: ubuntu-server-minimal
    search_drivers: false
  ssh:
    allow-pw: true
    authorized-keys: []
    install-server: true
  storage:
    config:
    - ptable: gpt
      serial: VBOX_HARDDISK_VB98cf2e3c-a3613d78
      path: /dev/sda
      wipe: superblock-recursive
      preserve: false
      name: ''
      grub_device: true
      type: disk
      id: disk-sda
    - device: disk-sda
      size: 1048576
      flag: bios_grub
      number: 1
      preserve: false
      grub_device: false
      offset: 1048576
      type: partition
      id: partition-0
    - device: disk-sda
      size: 2147483648
      wipe: superblock
      number: 2
      preserve: false
      grub_device: false
      offset: 2097152
      type: partition
      id: partition-1
    - fstype: ext4
      volume: partition-1
      preserve: false
      type: format
      id: format-0
    - device: disk-sda
      size: 24692916224
      wipe: superblock
      number: 3
      preserve: false
      grub_device: false
      offset: 2149580800
      type: partition
      id: partition-2
    - name: ubuntu-vg
      devices:
      - partition-2
      preserve: false
      type: lvm_volgroup
      id: lvm_volgroup-0
    - name: ubuntu-lv
      volgroup: lvm_volgroup-0
      size: 12343836672B
      wipe: superblock
      preserve: false
      type: lvm_partition
      id: lvm_partition-0
    - fstype: ext4
      volume: lvm_partition-0
      preserve: false
      type: format
      id: format-1
    - path: /
      device: format-1
      type: mount
      id: mount-1
    - path: /boot
      device: format-0
      type: mount
      id: mount-0
  updates: security
  version: 1
