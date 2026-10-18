# 01. Network Setup

Goal: all lab machines and my main PC live in one subnet so I can reach every VM directly (SSH / RDP / browser).

## Design

- Lab host: dedicated PC running the hypervisor, connected by **cable** (bridged mode is unreliable over Wi-Fi)
- Every VM uses a **Bridged** network adapter
- Static IPs outside the router's DHCP range

| Machine | IP |
|---|---|
| Main PC | 192.168.1.50 |
| Lab host | 192.168.1.100 |
| DC01 | 192.168.1.110 |
| WS01 | 192.168.1.120 |
| LNX01 | 192.168.1.130 |
| KALI | 192.168.1.140 |
| WAZUH | 192.168.1.150 |
| SOAR | 192.168.1.160 |

> Adjust the subnet and addresses to match your own router.

## Hypervisor settings

- **VirtualBox:** VM -> Settings -> Network -> Attached to: *Bridged Adapter* -> select the wired NIC
- **VMware Workstation:** VM -> Settings -> Network Adapter -> *Bridged* (check VMnet0 is bound to the wired NIC, not "Automatic")
- **Proxmox:** attach the VM to `vmbr0`

## Static IP on Ubuntu (netplan)

`/etc/netplan/00-lab.yaml`:

```yaml
network:
  version: 2
  ethernets:
    ens33:            # check the real name with: ip a
      dhcp4: false
      addresses: [192.168.1.150/24]
      routes:
        - to: default
          via: 192.168.1.1
      nameservers:
        addresses: [192.168.1.110, 192.168.1.1]
```

Apply: `sudo netplan apply`

## Verification

From the main PC:

```bash
ping 192.168.1.150
ssh user@192.168.1.150
```

Screenshots to add: hypervisor network settings, `ip a` output, successful ping/SSH.

![network settings](screenshots/01-network-settings.png)
