# Wireguard Ansible

This directory contains playbooks used for installing and configuring Wireguard VPN server.

[Ansible role by githubixx](https://github.com/githubixx/ansible-role-wireguard) was used as reference.

Tags:
```
- wg-generate-keys
- wg-config
- wgui-install
```

General options
```
wireguard_port: "51820"
wireguard_interface: "wg0"
wireguard_address: 10.16.0.1/24
wireguard_save_config: "true"
wireguard_postup:
  - iptables -t nat -A POSTROUTING -o {{ ansible_default_ipv4.interface }} -j MASQUERADE
wireguard_postdown:
  - iptables -t nat -D POSTROUTING -o {{ ansible_default_ipv4.interface }} -j MASQUERADE
```

Wireguard UI options
```
wgui_enabled: false
wgui_admin_user: admin
wgui_admin_password: pass
wgui_path: /opt/wireguard-ui
wgui_mtu: 1400

#User for wireguard ui service
wireguard_ui_user: wgui-admin

#Reverse proxy configuration
wgui_server_name: wgui.example.com
```