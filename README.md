*This project has been created as part of the 42 curriculum by aunoguei.*

# NetPractice

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
7. Alternatively, use the `Evaluation` tab to practice with random configurations.


The messages and logs displayed by the interface can be used to understand configuration problems, such as invalid addresses, incorrect subnet masks, missing routes, incorrect next hops, or missing reverse paths.

### Submission

The repository must contain:

- 10 exported configuration files, one for each level.
- All 10 configuration files placed at the root of the repository.
- All configuration files must be non-empty.
- This README.md file at the root of the repository.

During the defense, three random levels may be selected and must be successfully completed within the allocated time.

External tools are not allowed during the evaluation, except for simple calculators such as bc when permitted by the evaluation rules.

## Networking Fundamentals

  1. IPv4 Addresses

An IPv4 address consists of four octets: 

```
192.168.1.50
 │    │  │ │
 │    │  │ └── Host
 │    │  └───── Network
 └────┴──────── Network
```

However, the exact division between the network portion and the host portion is determined by the subnet mask.

```
IP address:   192.168.1.50/24
Mask:         255.255.255.0

              NETWORK          HOST
           ┌──────────────┬────────┐
           │ 192.168.1    │  .50   │
           └──────────────┴────────┘
```

Therefore:

```
Network:      192.168.1.0
First host:   192.168.1.1
Last host:    192.168.1.254
Broadcast:    192.168.1.255
```

Two devices can communicate directly when their IP addresses belong to the same subnet.

If they belong to different subnets, a router is required.


2. Subnet Masks and CIDR

A subnet mask determines which bits belong to the network and which belong to the host.

CIDR notation represents the number of network bits.

Examples:

/24 = 255.255.255.0
/25 = 255.255.255.128
/26 = 255.255.255.192
/27 = 255.255.255.224
/28 = 255.255.255.240
/29 = 255.255.255.248
/30 = 255.255.255.252

The larger the CIDR prefix, the smaller the subnet.

3. Subnetting Cheat Sheet

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

`/31` and `/32` are special cases and should not be treated as normal subnets.


### Network, Host and Broadcast Addresses

Every normal IPv4 subnet has three important types of addresses:

- **Network address** — the first address of the subnet. It identifies the network itself.
- **Usable host addresses** — the addresses between the network and broadcast addresses.
- **Broadcast address** — the last address of the subnet.

For example:

`192.168.1.128/26`

The subnet mask is:

`255.255.255.192`

The block size is:

`256 - 192 = 64`

Therefore the subnet is:

```text
Network:       192.168.1.128
First host:    192.168.1.129
Last host:     192.168.1.190
Broadcast:     192.168.1.191
```

### Hosts, Switches and Routers

1. Hosts on the Same Network

Devices connected to the same network can communicate directly.

```
Host A                         Host B
192.168.1.10/24               192.168.1.20/24
     │                              │
     └────────── Switch ────────────┘

Network: 192.168.1.0/24
```

Both devices belong to:

`192.168.1.0/24`

No router is required for their direct communication.

2. Different Networks Require a Router

A router connects different IP networks.

```
192.168.1.0/24                 10.0.0.0/24

 Host A                          Host B
192.168.1.10                    10.0.0.5
     │                              │
     │                              │
     └── Switch ── Router ── Switch ┘
                    │
              ┌─────┴─────┐
              │            │
       192.168.1.254   10.0.0.254
```

The router has an interface in each network:
```
Interface 1: 192.168.1.254/24
Interface 2: 10.0.0.254/24
```

This allows the router to forward packets between the two networks.

Internet access is not required for this. A router can connect private networks completely locally.

### Default Gateway

A default gateway is the router interface used by a host to reach destinations outside its local subnet.

Example:

```
Host A
IP:      192.168.1.10/24
Gateway: 192.168.1.254
```

Topology:

```
Host A
192.168.1.10
     │
     ▼
  Switch
     │
     ▼
Router
192.168.1.254
     │
     ▼
10.0.0.254
     │
     ▼
Host B
10.0.0.5
```

When Host A wants to reach:
`10.0.0.5`

it sees that 10.0.0.5 is outside its local subnet and sends the packet to its default gateway:
`192.168.1.254`

### Router Interfaces and Links

A router can have multiple interfaces, and each interface can belong to a different subnet.

For example:

```
Router

Interface 1 ── 192.168.1.254/24
Interface 2 ── 10.0.0.1/30
Interface 3 ── 172.16.0.1/24
```

The interfaces do not need to be in the same subnet.

However, two interfaces directly connected by the same link must normally belong to the same subnet.


```
Router A                         Router B

10.0.0.1/30 ─────── link ─────── 10.0.0.2/30

             Same subnet:
             10.0.0.0/30
```

### Point-to-Point Links and /30

A /30 subnet contains four addresses:

```
10.0.0.0/30

10.0.0.0  → Network
10.0.0.1  → Host
10.0.0.2  → Host
10.0.0.3  → Broadcast
```

This leaves exactly two usable addresses, which makes /30 useful for a point-to-point connection between two routers.

```
Router A                         Router B
10.0.0.1/30 ─────── link ─────── 10.0.0.2/30

             10.0.0.0/30
```

### Routing

A router uses a routing table to determine where packets should be sent.

A simplified routing table can look like:

```
Destination       Next Hop
192.168.1.0/24    directly connected
10.0.0.0/24       192.168.1.2
172.16.0.0/16     10.0.0.2
0.0.0.0/0         192.168.1.1
```

#### Destination Network

The destination network tells the router which network the packet should reach.

#### Next Hop

The next hop is the router/interface to which the packet should be forwarded next.

The next hop must be reachable from the router's current interface.

### Forward and Reverse Paths

A common NetPractice mistake is creating a valid path in only one direction.

Communication requires a valid route from the source to the destination and a valid route back.

```
Forward path:

Host A ───────> Router A ───────> Router B ───────> Host B



Reverse path:

Host A <─────── Router A <─────── Router B <─────── Host B

```

If the forward path works but the destination has no route back, the communication fails.

```
Host A ───────> Host B
                  ✓

Host A <─────── Host B
                  ✗
```

The return path may use:

a directly connected network;
a specific route;
a default route.

## Quick Problem-Solving Checklist

When solving a level, ask these questions in order:

1. What is the source?
2. What is the destination?
3. What subnet does each device belong to?
4. Are the IP addresses valid host addresses?
5. Are devices connected to the same link in the same subnet?
6. If the destination is remote, what is the gateway?
7. Does every router know the destination network?
8. Is every next hop reachable?
9. Can the destination route back to the source?
10. Check again.

This checklist is usually enough to solve most NetPractice configurations systematically.

## Resources

The resources below were used to study the concepts required for NetPractice. Each resource includes a short description of what it was used for.

### Training and project resources

- **42 NetPractice training interface** — interactive environment used to configure and test the 10 network levels.
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

- [YouTube — Routing Table Tutorial](https://www.youtube.com/watch?v=CGmTvukObOw)  
Used as a visual explanation of routing tables, destination networks, next hops, and packet forwarding.

- [YouTube — Routing Table Tutorial](https://www.youtube.com/watch?v=pCcJFdYNamc)  
Used as a visual explanation of the default gateway, including how a host forwards traffic destined for another network to its local router.

- [Cloudflare — What is a network switch?](https://www.cloudflare.com/learning/network-layer/what-is-a-network-switch/)  
  Used to understand switches, local networks, and the difference between **Layer 2 switches** and **Layer 3 routers**.

- [Cloudflare — What is DNS?](https://www.cloudflare.com/learning/dns/what-is-dns/)  
  Used to understand **DNS and the relationship between hostnames and IP addresses**. DNS was studied as supporting networking knowledge rather than as the main focus of NetPractice.

- [Practical Networking — Subnetting Mastery](https://www.practicalnetworking.net/stand-alone/subnetting-mastery/)  
  Used extensively to study **subnet masks, CIDR notation, subnetting, network addresses, broadcast addresses, usable host ranges, and calculating subnets**.



- [Geeksforgeeks — OSI Layers](https://www.geeksforgeeks.org/computer-networks/open-systems-interconnection-model-osi/)  
Used to study the **OSI model and its seven layers**, with particular attention to Layer 2 (Data Link) and Layer 3 (Network), which are relevant to switches, routers, MAC addresses, and IP addressing.

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
- Help organize, structure, proofread, and improve the README, including the description of the project, networking explanations, quick-reference material, and resource descriptions.

AI-generated explanations were reviewed and used as a learning aid. The final configurations were completed, tested, and verified through the NetPractice training interface.
