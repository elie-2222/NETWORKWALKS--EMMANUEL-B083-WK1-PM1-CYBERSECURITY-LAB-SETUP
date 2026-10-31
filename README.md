# scyber-B084C

# Cybersecurity Testing Lab Setup Using VirtualBox

## Project Overview

This project documents the setup and configuration of a basic cybersecurity testing lab using Oracle VirtualBox. The lab consists of Kali Linux as the testing machine and Windows 10 as the target machine.

The purpose of the lab is to create a controlled virtual environment where network communication, reconnaissance, security testing, and other cybersecurity practical exercises can be performed.

## Objectives

- Install and configure Kali Linux inside VirtualBox.
- Create a custom NAT Network for virtual machine communication.
- Configure static IP addresses for the virtual machines.
- Establish internet connectivity.
- Configure shared folders between the host and Kali Linux.
- Enable bidirectional clipboard and drag-and-drop.
- Install Windows 10 as a target machine.
- Test network communication between Kali Linux and Windows 10.

## Technologies and Tools

| Technology | Purpose |
|---|---|
| Linux Mint | Host operating system |
| Oracle VirtualBox | Virtualization platform |
| Kali Linux | Cybersecurity testing machine |
| Windows 10 | Target machine |
| NAT Network | Virtual network configuration |
| NetworkManager (nmcli) | Kali network configuration |
| Windows Command Prompt | Network configuration and testing |

## Lab Architecture

The lab uses a custom VirtualBox NAT Network named `NatNetwork`.

### Network Configuration

| Component | Configuration |
|---|---|
| Network Name | NatNetwork |
| Network Type | NAT Network |
| IPv4 Network | 10.0.0.0/24 |
| Gateway | 10.0.0.1 |
| DHCP | Enabled |
| IPv6 | Disabled |

### IP Addressing

| Machine | Role | IP Address |
|---|---|---|
| Kali Linux | Testing Machine | 10.0.0.2/24 |
| Windows 10 | Target Machine | 10.0.0.10/24 |
| NAT Gateway | Gateway | 10.0.0.1 |

## Implementation

### 1. Kali Linux Setup

Kali Linux was installed as a virtual machine in Oracle VirtualBox.

The virtual machine was connected to the custom NAT Network, and its network interface was configured with the static IP address `10.0.0.2/24`.

The network configuration was performed using NetworkManager:

```bash
sudo nmcli connection modify "eth0" \
ipv4.method manual \
ipv4.addresses 10.0.0.2/24 \
ipv4.gateway 10.0.0.1 \
ipv4.dns 8.8.8.8 \
ipv6.method disabled
```

The connection was restarted:

```bash
sudo nmcli connection down "eth0"
sudo nmcli connection up "eth0"
```

### 2. Shared Folder Configuration

A shared folder was configured between the Linux Mint host and Kali Linux.

Host directory:

`/home/eli/Downloads`

Kali Linux mount point:

`/media/sf_Downloads`

The shared folder was configured with read/write access and automatic mounting.

A test file was created to confirm access:

```bash
touch /media/sf_Downloads/kali_test.txt
echo "Shared folder is working" > /media/sf_Downloads/kali_test.txt
cat /media/sf_Downloads/kali_test.txt
```

### 3. VirtualBox Integration Features

The following integration features were configured:

- Shared Clipboard: Bidirectional
- Drag and Drop: Bidirectional
- Shared Folder: Enabled
- Automatic Mounting: Enabled

### 4. Windows 10 Setup

Windows 10 was installed as a second virtual machine.

Its network adapter was connected to the same `NatNetwork` used by Kali Linux.

A static IP address was configured:

- IP Address: `10.0.0.10`
- Subnet Mask: `255.0.0.0`
- Default Gateway: `10.0.0.1`
- Preferred DNS: `8.8.8.8`

The configuration was checked using:

```cmd
ipconfig
```

## Network Connectivity Testing

Communication between the two virtual machines was tested using the `ping` command.

From Kali Linux to Windows 10:

```bash
ping -c 4 10.0.0.10
```

From Windows 10 to Kali Linux:

```cmd
ping 10.0.0.2
```

Both tests were successful, confirming bidirectional network connectivity between the virtual machines.

## Results

The following outcomes were achieved:

- Successfully installed Kali Linux and Windows 10 in VirtualBox.
- Configured a custom NAT Network using the `10.0.0.0/24` subnet.
- Assigned static IP addresses to both virtual machines.
- Established internet access in Kali Linux.
- Configured shared folders between the host and Kali Linux.
- Enabled bidirectional clipboard and drag-and-drop.
- Successfully tested network communication between Kali Linux and Windows 10.
- Created an initial configuration snapshot for Kali Linux.

## Screenshots

Screenshots documenting the implementation and test results are included below.

Add your screenshots to a folder named `screenshots` in this repository.

Suggested evidence:

1. VirtualBox Manager showing both virtual machines.
2. NAT Network configuration.
3. Kali Linux network configuration.
4. Kali Linux internet connectivity.
5. Shared folder configuration and access.
6. Windows 10 running in VirtualBox.
7. Windows 10 IP configuration.
8. Successful ping from Kali Linux to Windows 10.
9. Successful ping from Windows 10 to Kali Linux.

Example image reference:

```markdown
![NAT Network Configuration](screenshots/nat-network.png)
```

## Future Improvements

The lab provides a foundation for further cybersecurity learning and practical exercises, including:

- Network reconnaissance using Nmap.
- Port scanning and service enumeration.
- Network traffic analysis using Wireshark.
- Vulnerability assessment.
- Windows security configuration and hardening.
- Practical exploration of network security concepts.

