# Campus Area Network (CAN) Design Using Cisco Packet Tracer

## Project Overview

This project demonstrates the design, configuration, and security of a **Campus Area Network (CAN)** using Cisco Packet Tracer. The network connects four departments—Admin, Lab1, Lab2, and Lab3—through a four-router topology with dedicated LAN switches, PCs, laptops, and servers.

The project focuses on reliable inter-network communication, dynamic IP address assignment, dynamic routing, network segmentation, and Layer 2 security.

## Objectives

- Design a multi-router campus network using Cisco Packet Tracer.
- Configure IP addressing and DHCP for automatic host configuration.
- Implement OSPF routing for communication between different LANs.
- Configure VLANs to organize network devices.
- Apply switch port security to limit unauthorized device connections.
- Configure Spanning Tree Protocol (STP), PortFast, and BPDU Guard.
- Enable SSH for secure remote router management.
- Apply and test access-control rules for the Admin network.
- Verify end-to-end connectivity and network security.

## Network Topology

The network consists of four routers connected in a diamond topology. Each router connects to a dedicated LAN containing a switch, end devices, and a server.

### Departments and IP Addressing

| Department | LAN Network | Default Gateway | VLAN |
|---|---|---|---|
| Admin | `192.168.10.0/24` | `192.168.10.1` | 10 |
| Lab1 | `192.168.20.0/24` | `192.168.20.1` | 20 |
| Lab2 | `192.168.30.0/24` | `192.168.30.1` | 30 |
| Lab3 | `192.168.40.0/24` | `192.168.40.1` | 40 |

Subnet mask for all LANs: `255.255.255.0`

### Inter-Router Addressing

The routers communicate over point-to-point links using `/30` subnets.

| Router Link | First Router IP | Second Router IP | Subnet |
|---|---|---|---|
| Admin – Lab1 | `10.0.56.1` | `10.0.56.2` | `10.0.56.0/30` |
| Admin – Lab3 | `10.0.58.1` | `10.0.58.2` | `10.0.58.0/30` |
| Lab1 – Lab2 | `10.0.67.1` | `10.0.67.2` | `10.0.67.0/30` |
| Lab2 – Lab3 | `10.0.78.1` | `10.0.78.2` | `10.0.78.0/30` |

Subnet mask for inter-router links: `255.255.255.252`

## Technologies Used

- **Cisco Packet Tracer** — Network design and simulation
- **Cisco Routers** — Inter-LAN routing and network connectivity
- **Cisco 2950-24 Switches** — LAN connectivity and Layer 2 security
- **OSPF** — Dynamic routing between routers
- **DHCP** — Automatic IP address assignment
- **VLANs** — Logical network segmentation
- **Port Security** — Restricting MAC addresses on switch access ports
- **STP** — Prevention of Layer 2 switching loops
- **PortFast and BPDU Guard** — Protection of end-device access ports
- **SSH** — Encrypted remote device management
- **Access Control Lists (ACLs)** — Traffic filtering between networks

## Implemented Network Features

### 1. Dynamic Routing with OSPF

OSPF is configured in area 0 to exchange routing information between the four routers.

Benefits:
- Automatic route discovery.
- Communication between different department LANs.
- Dynamic adaptation to supported routing changes.

### 2. DHCP Configuration

DHCP provides automatic IP address configuration to client devices.

Clients receive network settings such as:
- IP address.
- Subnet mask.
- Default gateway.

### 3. VLAN Configuration

Each department is assigned a separate VLAN on its local switch.

| Switch | VLAN ID | VLAN Name |
|---|---:|---|
| SW-ADMIN | 10 | ADMIN-LAN |
| SW-LAB1 | 20 | LAB1-LAN |
| SW-LAB2 | 30 | LAB2-LAN |
| SW-LAB3 | 40 | LAB3-LAN |

### 4. Switch Port Security

Port security is applied to designated PC access ports to restrict unauthorized devices.

Configured controls include:
- Maximum of one secure MAC address per protected port.
- Sticky MAC address learning.
- Shutdown violation mode.

The server and router uplink ports are kept separate from the PC port-security configuration.

### 5. Spanning Tree and Access-Port Protection

STP is enabled to prevent Layer 2 switching loops. PortFast is enabled on designated end-device ports, and BPDU Guard protects those ports against unexpected spanning-tree BPDUs.

### 6. Secure Remote Management

SSH is used for encrypted remote management of routers. Router access should be restricted to authorized management hosts wherever practical.

### 7. Admin Network Access Control

The intended security policy is:

- Admin devices may initiate permitted connections to Lab devices.
- Lab devices must not initiate new connections to Admin devices.
- Communication between Lab networks remains permitted where authorized.

This policy requires correctly configured and tested traffic filtering. Ordinary stateless ACLs do not provide complete connection tracking for every protocol.

## Testing and Verification

The following commands can be used to verify the network.

### Router Verification

```cisco
show ip interface brief
show ip route
show ip ospf neighbor
show ip protocols
show ip dhcp binding
show ip ssh
show access-lists
```

### Switch Verification

```cisco
show vlan brief
show port-security
show spanning-tree
show interfaces status
```

### PC Connectivity Tests

On each PC, open **Desktop → Command Prompt**.

Check IP configuration:

```text
ipconfig
```

Ping the local default gateway. For example, from an Admin PC:

```text
ping 192.168.10.1
```

Test communication with a host in another department using that host's actual IP address.

For security verification, test both permitted and denied connection directions. Confirm that the results match the intended ACL policy.

## How to Open the Project

1. Install Cisco Packet Tracer.
2. Clone or download this GitHub repository.
3. Open the included `.pkt` project file in Cisco Packet Tracer.
4. Inspect the router, switch, and end-device configurations.
5. Run the verification commands and connectivity tests.

## Repository Structure

```text
CAN-Cisco-Packet-Tracer/
├── README.md
├── CAN_Topology.pkt
└── images/
    └── topology.jpg
```

Rename the Packet Tracer file and screenshot to match this structure, or update the filenames in this README to match your actual files.

## Learning Outcomes

Through this project, I practiced:

- Designing and configuring multi-router networks.
- Implementing dynamic routing with OSPF.
- Configuring DHCP and IPv4 addressing.
- Organizing LANs using VLANs.
- Applying Layer 2 switch security.
- Configuring SSH and traffic filtering.
- Troubleshooting network connectivity.
- Validating network behavior using Cisco IOS commands.

## Future Enhancements

- Implement centralized network monitoring and logging.
- Introduce a dedicated management VLAN and restricted management access.
- Add redundant links and validate STP convergence.
- Implement stateful firewall controls for stronger inter-department isolation.
- Expand the topology with additional departments and services.

## Author

**Chaithan Koonapalli**

Computer Science Engineering — Cyber Security

SVCE, Tirupati

## Disclaimer

This is an educational network simulation created using Cisco Packet Tracer. Security behavior depends on the actual device configurations and the tests performed. The simulation does not, by itself, establish production-level security.
