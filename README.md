*This project has been created as part of the 42 curriculum by yucchen.*

# NetPractice 🌐

This project focuses on understanding how networks function at a fundamental level through hands-on problem solving.

## Description
NetPractice is a networking project that introduces the basics of computer networks.

The goal is to understand how devices communicate by learning how to configure IP addresses, use subnet masks, connect networks through routers, and understand the role of a default gateway. 

This project is completed through a training interface in which each level presents a network configuration problem. The objective is to solve each problem by making the network function correctly.

## Instructions

### Run the training interface
```bash
python3 -m http.server 49242 
```
You may change the port number if needed.

Then open your web browser and go to the URL:
```bash
http://localhost:49242
```

### Export configurations
For each level, export the configuration file by clicking the `Get my config` button.

### Submission requirements
There are 10 levels in the training interface, so you must submit 10 configuration files, one for each level.

Requirements:
- Place all 10 files at the root of the repository
- Enter your login in the training interface before exporting the files

## Networking Concepts & Resources
### TCP (Transmission Control Protocol) / IP (Internet Protocol) Addressing
TCP/IP addressing is the system used to identify devices on a network and route data between them.
It is part of the TCP/IP model, which is the foundation of how the Internet works.

In simple terms:
> TCP/IP addressing = How devices get an address (IP) + how data knows where to go (routing using that address)

> IP Address = "Where am I?"

An IP address uniquely identifies a device on a network.

Example:
```bash
192.168.1.10
```
You can think of it like a home address:
- `192.168.1` -> the network
- `.10` -> the host (device)

TCP/IP addressing includes:
- IP address
- Subnet mask
- Network address
- Broadcast address
- Default gateway
- Routing rules

TCP/IP addressing is how devices are identified and how data is routed across networks using IP addresses and subnet logic.

Useful resources:
- https://www.geeksforgeeks.org/computer-networks/tcp-ip-model/
- https://learn.microsoft.com/en-us/troubleshoot/windows-client/networking/tcpip-addressing-and-subnetting

### Subnet Mask
A subnet mask tells us which part of an IP address represents the network and which part represents the host.

Example:
```bash
IP address:							  192.168.1.10
Subnet mask:						  255.255.255.0
CIDR (Classless Inter-Domain Routing): /24
```
For `/24`:
- Network part: first 24 bits
- Host part: last 8 bits

Subnet masks are essential for determining:
- the network address
- the broadcast address
- the valid host range
- whether two devices are in the same subnet

#### Broadcast Address
A broadcast address is a special IP address used to send a message to all devices in the same network at once.

Example:
```bash
IP address:	 192.168.1.10
Subnet mask: 255.255.255.0 (/24)
```
- Network range: `192.168.1.0 - 192.168.1.255`
- Broadcast address: `192.168.1.255`

The broadcast address is the last address in the subnet.
It is formed by setting all host bits = 1
```bash
11111111 = 255
```
- You cannot assign a broadcast address to a device
- It is reserved for network-wide communication

Compare with Other Addresses
Type 	 	      | Example		  | Purpose           	   |
------------------|---------------|------------------------|
Network address   | 192.168.1.0   | identifies the network |
Host address      | 192.168.1.10  | identifies a device    |
Broadcast address | 192.168.1.255 |	send to all devices    |

Useful resources:
- https://www.calculator.net/ip-subnet-calculator.html
- https://www.aelius.com/njh/subnet_sheet.html

### Default Gateway
A default gateway is the device, usually a router, that a computer uses to send data to other networks.

In simple terms:
> Default gateway = "the exit door of the local network"

If your computer doesn't know where to send data, it sends it to the gateway.

Example:
```bash
IP address: 192.168.1.10
Mask:	 	255.255.255.0 (/24)
Gateway: 	192.168.1.1
```
This means:
- the local network is `192.168.1.x`
- the router is `192.168.1.1`

How It Works

When you send data:
1. Check: Is destination in the same subnet?
2. If YES -> send directly
3. If NO -> send the packet to the default gateway

Case 1: Same network
```bash
192.168.1.20
```
-> Directly send (no gateway needed)

Case 2: Different network
```bash
8.8.8.8 
```
-> Not in your network

-> Send to default gateway (192.168.1.1)

Then:
- Router takes over
- Forwards packet to the Internet

How to Find Your Default Gateway

Linux: Type `ip route` or `route -n` in the terminal.

Real-Life Analogy
- Your device = your house
- Local network = your neighborhood
- Default gateway = the main road out of your neighborhood

If you go to your neighbor -> no need for main road

If you go to another city -> you must go through the main road

A default gateway is the router your device uses to send data outside its local network.

Useful resources:
- https://www.cbtnuggets.com/blog/technology/networking/what-is-default-gateway
- What is the Role of the Default Gateway? (https://www.youtube.com/watch?v=2VtnlpLKp8I)
- https://www.sciencedirect.com/topics/computer-science/default-gateway

### Routers and Switches
Routers and switches are both network devices, but they have different roles.

#### Switch 

A switch connects devices within the same local network (LAN).

What it does:
- Connects computers, printers, and other devices
- Sends data inside the same network
- Uses MAC addresses (hardware addresses)

Example:
- Laptop -> 192.168.1.10
- Phone -> 192.168.1.20

Devices in the same network can communicate through a switch.
No router needed.

Behavior:
- learns which device is connected to which port
- sends data only to the correct device

#### Router 

A router connects different networks together.

What it does:
- Connects a local network to other networks or the Internet
- Decides where data should go
- Uses IP addresses

Example:
```bash
8.8.8.8
```
This address is not in the local network, so:

-> send to router (default gateway)

-> router forwards it to the Internet

Behavior:
- checks the destination IP address
- uses a routing table
- forwards the packet to next network

Switch vs Router
Feature 	 | Switch			   | Router           |
-------------|---------------------|------------------|
Scope        | Same network (LAN)  | Between networks |
Address type | MAC address		   | IP address		  |
Main role	 | Connect devices	   | Route traffic	  |
Used for	 | Local communication | Internet access  |

- Same subnet -> Switch
- Different subnet -> Router (gateway)

Switch connects devices within a network; router connects different networks and forwards data between them.

Useful resources:
- https://developerhelp.microchip.com/xwiki/bin/view/applications/tcp-ip/routers-switches-addressing/
- https://www.cisco.com/c/en_uk/solutions/small-business/resource-center/networking/network-switch-vs-router.html
- https://www.geeksforgeeks.org/computer-networks/difference-between-router-and-switch/

### OSI (Open Systems Interconnection) Layers
The OSI model organizes network communication into 7 layers.

It helps explain how data moves from one computer to another step by step.

The 7 OSI Layers (Top -> Bottom)
Layer	| Name		   | Function							    |
--------|--------------|----------------------------------------|
 7		| Application  | User-level apps (browser, email)       |
 6		| Presentation | Format, encryption, encoding	        |
 5		| Session	   | Manage connections (start/stop)        |
 4		| Transport	   | Reliable delivery (TCP/UDP)            |
 3		| Network	   | IP address, routing, default gateway   |
 2		| Data Link	   | MAC addresses, switches			  	|
 1		| Physical	   | Cables, electrical or wireless signals |

How Data Flows

When sending data:
1. The application creates the data
2. Each layer adds its own information (headers)
3. The data is sent through the network
4. The receiver processes it layer by layer

Real-Life Analogy

Sending a package:
Step		   		   | OSI Layer    |
-----------------------|--------------|
Write message  		   | Application  |
Put in format  		   | Presentation |
Start delivery         | Session	  |
Choose delivery method | Transport	  |
Add address			   | Network	  |
Choose local route	   | Data Link	  |
Physically send		   | Physical	  |

Easy Way to Remember

From top to bottom (Application -> Physical): All People Seem To Need Data Processing

OSI layers divide networking into 7 steps, helping us understand how data is sent, addressed, and delivered across networks.

Useful resources:
- https://www.geeksforgeeks.org/computer-networks/open-systems-interconnection-model-osi/
- https://www.imperva.com/learn/application-security/osi-model/
- https://www.networkacademy.io/ccna/network-fundamentals/understanding-the-osi-model

### How AI was Used
AI tools were used as a learning aid to help review networking concepts.

## Submission Details
The final submission must include 10 exported configuration files, one for each level, placed at the repository root.
