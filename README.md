Role Name
=========

An Ansible role to install KVM host. It is possible to create bridges on the host with this role and also create vritual networks in libvirt and connect them to the bridges. Also it is possible to create storage pools as part of installation.

Requirements
------------

No specific requirements.

Role Variables
--------------

```ansible

# The network brigdes to be created on the host
# The syntax is:
# BRIDGE_NAME:
#   ip4: IP/PREFIX
#   gw4: GW IP
#   slave: Physical interface name
# Example:
# kvm-br0:
#    ip4: 192.168.0.21/24
#    gw4: 192.168.0.1
#    slave: enp3s0
kvm_network_bridges: []

# The virtual networks to be added
# The syntax is:
# NETWORK_NAME:
#   mode: bridge
#   bridge: BRIDGE_NAME
# Example:
# virbr0:
#   mode: bridge
#   bridge: kvm-br0
kvm_virtual_networks: []

# The storage pools to be added
# The syntax is:
# POOL_NAME:
#   capacity: SIZE in byte
#   path: PATH
# Example:
# kvm-images:
#   capacity: 536870912000
#   path: /var/lib/libvirt/images

kvm_pools: []


```

Dependencies
------------

N/A

Example Playbook
----------------

```ansible
- name: Install KVM
  hosts: localhost
  vars:
    kvm_network_bridges:
      kvm-br0:
        ip4: 192.168.0.21/24
        gw4: 192.168.0.1
        slave: enp3s0
    kvm_virtual_networks:
      virbr1:
        mode: bridge
        bridge: kvm-br0
    kvm_pools:
      kvm-images:
        capacity: 536870912000
        path: /var/kvm-images
  roles:
    - role: siavashoutadi.kvm
```

License
-------

Apache
