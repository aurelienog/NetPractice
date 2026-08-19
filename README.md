*This project has been created as part of the 42 curriculum by aunoguei.*

## Description

NetPractice is a practical networking exercise from the 42 curriculum designed to introduce the basics of computer networking.

The goal of the project is to configure small-scale simulated networks so that they function correctly. The exercises focus on understanding and configuring IP addresses, subnet masks, default gateways, routers, and switches.

The project consists of 10 levels. Each level presents a non-functioning network configuration with one or more objectives. The configuration must be modified until the network works correctly.

Through this project, I studied the fundamentals of TCP/IP addressing and learned how devices communicate within the same network and through routers when communicating with different networks.

## Instructions

### Running the training interface

First, extract the project files into a directory of your choice.

Run the provided `run.sh` script:

```bash
./run.sh
```

This starts a local web server and opens the NetPractice training interface in a web browser.

If `run.sh` does not work correctly, the interface can be started manually with:

```bash
python3 -m http.server 49242
```

Then open the following address in a web browser:

```text
http://localhost:49242
```

The port can be changed if necessary.

### Practicing the levels

The training interface contains 10 levels.

1. Enter the login in the training interface.

For each level:
 * 2. Analyze the network diagram and the objectives.
 * 3. Modify the available configuration fields.
 * 4. Use **Check again** to verify the configuration.
 * 5. When the level is successfully completed, use **Get my config** to export the configuration.
 * 6. Save the exported configuration file in the repository before moving to the next level.

The logs displayed at the bottom of the interface can be used to identify configuration problems, such as invalid IP addresses or missing gateways.

### Submission

The repository must contain **10 exported configuration files**, one for each level.

All 10 configuration files must be placed at the **root of the repository**.

The repository must also contain this `README.md` file at its root.

During the defense, three random levels must be successfully completed within a limited amount of time. External tools are not allowed during the evaluation, although a simple calculator such as `bc` is tolerated.

## Networking Concepts Studied

The main networking concepts studied during this project are:

* **TCP/IP addressing** — understanding IPv4 addresses and how devices are addressed within a network.
* **Subnet masks** — determining which part of an IP address identifies the network and which part identifies the host.
* **Subnetting** — dividing networks into smaller subnets and determining which devices belong to the same network.
* **Default gateways** — understanding how devices communicate with destinations outside their local network.
* **Routers** — understanding how routers connect different networks and how their interfaces belong to different networks.
* **Switches** — understanding their role in connecting devices within a network.
* **OSI layers** — understanding the basic networking model and the relationship between networking concepts and layers.
## Resources

The following resources were used to study and understand the networking concepts required for this project.

### Networking Concepts Studied

The main networking concepts studied during the project were:

* **TCP/IP addressing** — understanding IPv4 addresses and how devices are addressed within a network.
* **Subnet masks** — understanding how a subnet mask separates the network portion from the host portion of an IP address.
* **Subnetting** — dividing networks into smaller subnets and determining which IP addresses belong to each network.
* **Network and broadcast addresses** — identifying the network address and broadcast address of a subnet.
* **Default gateways** — understanding how a device communicates with destinations outside its local network.
* **Routers** — understanding how routers connect different networks and how their interfaces are configured with IP addresses.
* **Switches** — understanding their role in connecting devices within the same local network.
* **OSI layers** — understanding the basic OSI model and the relationship between networking devices and layers, particularly Layer 2 (Data Link) and Layer 3 (Network).
* **Hosts and networks** — understanding the relationship between individual hosts, their IP addresses, and the networks to which they belong.

### Articles and Documentation

* [Cloudflare — What is TCP/IP?](https://www.cloudflare.com/es-es/learning/ddos/glossary/tcp-ip/)
  Used to study **TCP/IP addressing** and the fundamentals of communication between devices.

* [Cloudflare — What is My IP Address?](https://www.cloudflare.com/learning/dns/glossary/what-is-my-ip-address/)
  Used to reinforce the understanding of **IP addresses**.

* [Cloudflare — What is the Internet Protocol (IP)?](https://www.cloudflare.com/es-es/learning/network-layer/internet-protocol/)
  Used to study **IP addressing** and the **Network layer**.

* [Cloudflare — What is DNS?](https://www.cloudflare.com/learning/dns/what-is-dns/)
  Used to understand the role of **DNS** in computer networks.

* https://www.cloudflare.com/learning/network-layer/what-is-a-router/

* https://www.cloudflare.com/learning/network-layer/what-is-a-network-switch/

* https://www.youtube.com/watch?v=htQXaoHTSmE

* [Practical Networking — Subnetting Mastery](https://www.practicalnetworking.net/stand-alone/subnetting-mastery/)
  Used to study **subnetting, subnet masks, network addresses, broadcast addresses, and host ranges**.

### Exercise Resources

* [Subnetting.net](https://www.subnetting.net/)
  Used to practice **subnetting, CIDR notation, subnet masks, network addresses, and host ranges**.

* [SubnetIPv4](https://subnetipv4.com/)
  Used to practice **IPv4 addressing and subnetting**.

### AI Usage

AI tools were used as a learning aid during the project.

They were used to:

* Clarify networking concepts such as **TCP/IP addressing, subnet masks, subnetting, default gateways, routers, switches, and OSI layers**.
* Provide additional explanations and examples when a networking concept was difficult to understand.
* Help identify and understand mistakes encountered while solving the exercises.
* Support the learning process and reinforce concepts studied through the external resources listed above.

AI-generated information was reviewed and used only when it was understood. The configurations submitted for the project were solved and verified through the NetPractice training interface.
