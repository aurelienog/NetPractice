*This project has been created as part of the 42 curriculum by aunoguei.*

## Description

NetPractice is a practical networking exercise from the 42 curriculum designed to introduce the fundamentals of computer networking.

The primary objective is to configure small-scale simulated networks so that they function correctly. The exercises focus on IPv4 addressing, subnet masks, subnetting, network and broadcast addresses, default gateways, routers, switches, and routing tables.

The project consists of 10 levels. Each level presents a non-functioning network topology with one or more objectives. The configuration must be modified until the required communication paths work correctly.

Through this project, I studied how devices communicate within the same subnet, how routers connect different IP networks, how routing tables determine the next hop, and why communication requires a valid path in both directions.

## Instructions

### Running the training interface

1. Download the file attached to the project’s page on the intranet.

2. Extract the files into any folder of your choice.

3. Run the provided script from your terminal:

Run the provided script to the local NetPractice training interface.

```bash
./run.sh
```

If `run.sh` does not work correctly, the interface can be started manually with:

```bash
python3 -m http.server 49242
```

Then open your browser and navigate to: 
```text
http://localhost:49242
```

The port may be changed if necessary.

### Practicing the levels

The training interface contains 10 levels.

1. Enter the login in the training interface and press `Start!`.
2. Analyze the network topology before changing values.
3. Configure the required IP addresses, subnet masks, gateways, and routes modifying the unshaded fields.
4. Use `Check again` to verify the configuration.
5. When the level is successfully completed, use `Get my config` to export the configuration.
6. Save the exported configuration file in the repository before moving to the `Next level`.
7. Alternatively, use the Evaluation tab to practice with random configurations


The messages and logs displayed by the interface can be used to understand configuration problems, such as invalid addresses, incorrect subnet masks, missing routes, incorrect next hops, or missing reverse paths.

### Submission

The repository must contain **10 exported configuration files**, one for each level.

All 10 configuration files must be placed at the **root of the repository** and must not be empty.

The repository must also contain this `README.md` file at its root.

During the defense, three random levels may be selected and must be successfully completed within the allocated time. External tools are not allowed during the evaluation, except for simple calculators such as `bc` when permitted by the evaluation rules.

## Networking Concepts Studied

The project covers the following networking concepts:

- **TCP/IP addressing** — identifying devices and networks using IPv4 addresses.
- **Subnet masks** — determining which part of an IPv4 address identifies the network and which part identifies the host.
- **CIDR notation** — representing subnet masks using prefixes such as `/24`, `/26`, `/30`, etc.
- **Subnetting** — dividing an address space into smaller networks.
- **Network addresses** — identifying the first address of a subnet, which represents the subnet itself.
- **Host addresses** — identifying usable addresses assigned to devices such as hosts and router interfaces.
- **Broadcast addresses** — identifying the last address of an IPv4 subnet, which is reserved for broadcast communication.
- **Default gateways** — forwarding traffic from a local subnet toward destinations outside that subnet.
- **Routers** — connecting different IP networks and forwarding packets according to routing tables.
- **Routing tables** — associating destination networks with next hops.
- **Switches** — connecting devices within a local network and forwarding traffic at the data-link layer.
- **OSI layers** — understanding the seven-layer networking model, especially Layer 2 (Data Link) and Layer 3 (Network).
- **Reverse paths** — understanding that successful communication requires a return path from the destination to the source.


## Quick Reference

### Subnetting Cheat Sheet

The block size determines the increment between subnet network addresses.

| **Block Size** | `128` | `64` | `32` | `16` | `8` | `4` | `2` | `1` |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Subnet Mask** | `128` | `192` | `224` | `240` | `248` | `252` | `254` | `255` |
| **CIDR (4th octet)** | `/25` | `/26` | `/27` | `/28` | `/29` | `/30` | `/31` | `/32` |
| **CIDR (3rd octet)** | `/17` | `/18` | `/19` | `/20` | `/21` | `/22` | `/23` | `/24` |
| **CIDR (2nd octet)** | `/9` | `/10` | `/11` | `/12` | `/13` | `/14` | `/15` | `/16` |
| **CIDR (1st octet)** | `/1` | `/2` | `/3` | `/4` | `/5` | `/6` | `/7` | `/8` |

For normal IPv4 subnets:

- `/30` → 4 addresses, 2 usable host addresses
- `/29` → 8 addresses, 6 usable host addresses
- `/28` → 16 addresses, 14 usable host addresses
- `/27` → 32 addresses, 30 usable host addresses
- `/26` → 64 addresses, 62 usable host addresses
- `/25` → 128 addresses, 126 usable host addresses
- `/24` → 256 addresses, 254 usable host addresses

`/31` and `/32` are special cases and should not be treated as normal subnets with network, host and broadcast addresses.


### Network, Host and Broadcast Addresses

Every subnet has three important types of addresses:

- **Network address** — the first address of the subnet. It identifies the network itself.
- **Usable host addresses** — the addresses between the network and broadcast addresses.
- **Broadcast address** — the last address of the subnet.

For example:

`192.168.1.128/26`

The block size is:

`256 - 192 = 64`

Therefore the subnet is:

```text
Network:       192.168.1.128
First host:    192.168.1.129
Last host:     192.168.1.190
Broadcast:     192.168.1.191
```

### Core Mechanics Visualized

1. IP Address Anatomy (Network vs. Host)An IP address is split into a Network portion and a Host portion based on the Subnet Mask. Devices can only talk directly if they share the exact same Network ID.

```text
IP address:      192.168.1.50/24
Subnet mask:     255.255.255.0

                 NETWORK          HOST
              ┌──────────────┬────────┐
              │ 192.168.1    │  .50   │
              └──────────────┴────────┘

Network:       192.168.1.0
First host:    192.168.1.1
Last host:     192.168.1.254
Broadcast:     192.168.1.255
```

```
192.168.1.130/26

Mask: 255.255.255.192

Group size:
256 - 192 = 64

Subnets:

192.168.1.0   - 192.168.1.63
192.168.1.64  - 192.168.1.127
192.168.1.128 - 192.168.1.191  ← IP belongs here
192.168.1.192 - 192.168.1.255

Therefore:

Network:    192.168.1.128
First host: 192.168.1.129
IP:         192.168.1.130
Last host:  192.168.1.190
Broadcast:  192.168.1.191
```

2. Default Gateways & Routers

```text
 [Host A] (192.168.1.10/24)
    │
    ▼ (Wants to reach 10.0.0.5)
 [Local Switch]
    │
    ▼ 
 [Router] ── Interface 1 (Gateway): 192.168.1.254
    │     ── Interface 2:            10.0.0.254
    ▼ 
 [Remote Switch]
    │
    ▼ 
 [Host B] (10.0.0.5/24)
```

3. The Reverse Path Rule

For communication to succeed, a valid return path must exist from the destination back to the source. This path may be provided by a directly connected route, a specific route, or a default route.

```text
Forward path:

Host A ───────> Router ───────> Host B
                   ✓


Return path:

Host A <─────── Router <─────── Host B
                   ✓

Both directions must have a valid path.
```


---

### Why /30 is commonly used between routers

```markdown

A `/30` subnet contains 4 addresses:

    Network
    Host
    Host
    Broadcast

Example:

    10.0.0.0/30

    10.0.0.0  → Network
    10.0.0.1  → Host
    10.0.0.2  → Host
    10.0.0.3  → Broadcast

Therefore a point-to-point link can use:

    Router A: 10.0.0.1/30
    Router B: 10.0.0.2/30

Both interfaces belong to the same subnet:

    10.0.0.0/30
```

## Resources

The resources below were used to study the concepts required for NetPractice. Each resource includes a short description of what it was used for.

### Training and project resources

- **42 NetPractice training interface** — the interactive environment used to configure and test all 10 network levels.
- **42 NetPractice subject / provided project files** — used to understand the project requirements, execution procedure, level format, and submission requirements.
- **`run.sh`** — provided script used to start the local training interface.

### Networking documentation

- [Cloudflare — What is TCP/IP?](https://www.cloudflare.com/es-es/learning/ddos/glossary/tcp-ip/)  
  Used to study the **TCP/IP model, IP communication, and the fundamentals of network communication**.

- [Cloudflare — What is My IP Address?](https://www.cloudflare.com/learning/dns/glossary/what-is-my-ip-address/)  
  Used to reinforce the concepts of **IP addresses, public/private addressing, and identifying devices on networks**.

- [Cloudflare — What is the Internet Protocol (IP)?](https://www.cloudflare.com/es-es/learning/network-layer/internet-protocol/)  
  Used to study **IPv4 addressing and the IP Network Layer**, including how IP packets are addressed.

- [Cloudflare — What is routing?](https://www.cloudflare.com/learning/network-layer/what-is-routing/)  
  Used to understand **routing, routing tables, destination networks, next hops, and how routers select paths between networks**.

- [Cloudflare — What is a router?](https://www.cloudflare.com/learning/network-layer/what-is-a-router/)  
  Used to study **routers, their role in connecting different IP networks, and how routing tables are used to forward packets**.

- [Cloudflare — What is a network switch?](https://www.cloudflare.com/learning/network-layer/what-is-a-network-switch/)  
  Used to understand **switches, local networks, Layer 2 communication, and the difference between switches and routers**.

- [Cloudflare — What is DNS?](https://www.cloudflare.com/learning/dns/what-is-dns/)  
  Used to understand **DNS and the relationship between hostnames and IP addresses**. DNS was studied as supporting networking knowledge rather than as the main focus of NetPractice.

- [Practical Networking — Subnetting Mastery](https://www.practicalnetworking.net/stand-alone/subnetting-mastery/)  
  Used extensively to study **subnet masks, CIDR notation, subnetting, network addresses, broadcast addresses, usable host ranges, and calculating subnets**.

- [YouTube — routing table]( https://www.youtube.com/watch?v=CGmTvukObOw)

### Subnetting practice tools

- [Subnetting.net](https://www.subnetting.net/)  
  Used as an interactive tool to practice **subnetting, CIDR notation, subnet masks, network addresses, broadcast addresses, and usable host ranges**.

- [SubnetIPv4](https://subnetipv4.com/)  
  Used to practice **IPv4 subnet calculations, subnet masks, CIDR notation, and determining valid host addresses**.

### Supplementary video resource

- [YouTube — supplementary networking tutorial](https://www.youtube.com/watch?v=htQXaoHTSmE)  
  Used as an additional visual explanation of **networking and subnetting concepts** while studying the project.

## AI Usage

AI tools were used as a learning aid during the project.

They were used to:

- Clarify networking concepts such as **TCP/IP addressing, subnet masks, subnetting, network and broadcast addresses, default gateways, routers, routing tables, switches, and OSI layers**.
- Provide additional explanations and examples when a networking concept was difficult to understand.
- Help analyze and understand mistakes encountered while solving the NetPractice exercises.
- Explain routing concepts such as **next hops, communication between different subnets, default routes, and reverse paths**.
- Reinforce concepts studied through the external resources listed in this README.

AI-generated explanations were reviewed and used as a learning aid. The final configurations were completed, tested, and verified through the NetPractice training interface.
