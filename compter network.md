**Computer Networks (CN) for DevOps** 
1. The Physical Internet — How the Internet Works
2. Internet Addressing
3. How Data Moves on the Internet
4. Internet and Network Security
5. System Design — How to Design an Application

# 🌐 1. What Is the Internet?

Imagine one laptop in Pune, one laptop in Delhi, and another laptop in Canada.

If you use a computer independently without connecting it to another device or network, it is called a **standalone computer**.

When a device connects to other devices and communicates with them, these connected devices form a **computer network**.

When multiple computer networks around the world connect and communicate with each other, they form the **Internet**.

## How Are All These Devices Connected?

Devices connect to the Internet through different types of networks and communication technologies.

Much of the Internet's data travels through **fiber-optic cables**, including cables laid under the ocean. These cables use light to transmit data over long distances.

**For example:**
- A laptop in Pune connects to the Internet through a local network and an Internet Service Provider (ISP).
- A laptop in Canada connects through its own network and ISP.
- These networks communicate with each other through routers and physical communication links.

**In simple words:** The Internet connects computers and networks around the world so they can exchange data.

Packet, Latency, and Bandwidth
**1. Packet:** A packet is a small logical unit of data. It contains encoded data and address details that help it travel from the source to the destination.

**2. Latency:** Latency is the time it takes for data to travel from the source to the destination.

**3. Bandwidth:** Bandwidth is the maximum amount of data that a network can transfer per second, such as Mbps or Gbps.


Jitter: The variation in latency (delay) when data packets travel from the source to the destination is called jitter.

Simple example:

**Packet**: A small piece of data sent over the internet.

**Latency**: How long the data takes to reach its destination.

**Bandwidth**: How much data can be transferred per second

**jitter**-If one packet takes 20 ms, the next takes 40 ms, and another takes 25 ms, this variation in delay is called jitter.

physical 

router , switch, hub



Data is transmitted between different networks. When a data packet reaches your home network, a router is needed to forward it to the correct device.
## 🌐 Physical Network Devices

### 1. Router
A **router** forwards packets to the correct network.

- It connects different networks.
- It helps data travel from one network to another.
- When data reaches your home network from the Internet, your home router helps deliver it to the correct device.

### 2. Switch
A **switch** is a physical networking device that connects multiple devices within the same local network.

- You can connect multiple computers, laptops, and other devices to a switch.
- It allows connected devices to communicate with each other.
- A switch can help multiple devices access the Internet when connected to a router.


A **hub**is an old networking device used to connect multiple computers in a network.
- Before switches became common, hubs were used to connect multiple devices.
- When a hub receives data from one device, it sends that data to all connected devices.
- A switch is smarter because it forwards data to the specific device it is intended for.
**Simple example:** A hub is like a teacher announcing a message to the whole class, while a switch is like delivering the message only to the intended student.



**CDN (Content Delivery Network)**
A CDN is a network of servers that delivers static content to users from a server located closer to them.
Static data means files that usually remain the same, such as images, CSS, JavaScript files, videos, and fonts.

**Example:**
- Your main website server is in the USA.
- A user opens your website in India.
- A CDN can deliver images and CSS files from a nearby Indian CDN server instead of fetching them from the USA every time.
- This reduces latency and helps the website load faster.
  
**Edge computing**: Processing data closer to the user or device instead of sending everything to a central server.

**Simple difference:**
- **CDN: Delivers**cached content closer to the user.
- **Edge computing**: Processes data closer to the user.

### 2. Internet Addressing

Internet addressing is a system used to uniquely identify devices on a network.

For example, if I send data from Pune to Delhi, the data needs the correct destination address. If the address is incorrect, the data may reach the wrong destination or fail to reach its destination.

IP (Internet Protocol) is a set of rules used to address and route data packets across networks. Every device communicating over an IP network uses IP addresses to identify the source and destination of data.

**Key Point:** An IP address helps data reach the correct destination over the internet.


**1. IPv4 (Internet Protocol Version 4)**

Address size: 32 bits

Total addresses: Approximately 4.3 billion

Format: 4 octets separated by dots (.)

Range of each octet: 0–255

Example: 192.168.1.4

Example breakdown:

192 . 168 . 1 . 4

Each octet contains 8 bits, so (4 \times 8 = 32) bits.

**2. IPv6 (Internet Protocol Version 6)**

Address size: 128 bits

Total addresses: Approximately (3.4 \times 10^{38}) (340 undecillion)

Format: 8 groups of hexadecimal numbers separated by colons (:)

Example: 2001:0db8:0000:0000:0000:ff00:0042:8329

Each group contains 16 bits, so (8 \times 16 = 128) bits.


**3. Subnet (Subnetwork)**

A subnet is a smaller network created by dividing a larger IP network into smaller networks.

IPv4 supports approximately 4.3 billion addresses. Instead of managing all devices in one large network, we divide the network into smaller parts called subnets.

Example:

Large network: 192.168.1.0/24

Subnet 1: 192.168.1.0/26

Subnet 2: 192.168.1.64/26

Each subnet has its own IP address range.

**Key Point:** A subnet helps organize IP addresses and control how devices communicate within a network. Devices outside the subnet generally need a router to communicate with devices inside it.



## CIDR (Classless Inter-Domain Routing)

A subnet is a smaller network within a larger network. CIDR helps define the size of a subnet and its IP address range.

Question: If a subnet is running internally, how can we find the IP address range available within that subnet?


**4. DNS (Domain Name System)**

DNS is like a phone book of the internet.

DNS translates a human-readable domain name into an IP address so that a browser can locate the correct server.

Example:

Domain name: google.com

DNS finds the IP address associated with google.com.

The browser uses that IP address to connect to Google's server.

**Key Point:** Humans remember domain names easily, while computers use IP addresses to communicate. DNS connects the two.


**Step-by-Step DNS Lookup Flow**

**Example:** You type google.com into your browser.

**User enters the domain:** You type google.com in your browser.

**Browser cache**: The browser checks whether it already knows the IP address.

**Operating system cache:** If not found, the OS checks its DNS cache.

**Recursive DNS resolver:** The request goes to a DNS resolver, usually provided by your ISP or a public DNS service.

**Root DNS server:** If the resolver has no cached answer, it asks a root server where to find .com DNS servers.

**TLD DNS server:** The .com server directs the resolver to Google's authoritative DNS servers.

**Authoritative DNS server:** It provides the DNS record containing the IP address for google.com.

**IP address returned:** The resolver sends the answer back to your computer and may cache it.

**Browser connects:** The browser uses the IP address to connect to Google's server and load the website.



## 3. How Data Moves on the Internet

### OSI Model – Daily Life Story (Teacher & Student on WhatsApp)

**Example:** A student sends “Hello, Sir!” to a teacher on WhatsApp.

**Which layer does application work in OSI?**

**1. Application Layer — WhatsApp**

The student types “Hello, Sir!” and presses Send.

Layer 7 · User-facing application

**Which layer does encryption work in OSI?**

**2. Presentation Layer — Data Format**

The message is represented in a suitable data format and encrypted for secure communication.

Layer 6 · Formatting and encryption

**Which layer does authentication work in OSI?**

**3. Session Layer — Communication Session**

Think of this as managing the ongoing communication between the two endpoints.

Layer 5 · Session management

**Which layer does device address MAC address exchange work in OSI?**

**4. Transport Layer — TCP/UDP**

Transport protocols help deliver data between endpoints. WhatsApp can use different transport mechanisms depending on the connection and service.

Layer 4 · Transport

**Which layer does IP exchange work in OSI?**

**5. Network Layer — IP Address**

IP addressing and routing help move packets across networks toward their destination.

Layer 3 · IP routing

**Which layer does work in OSI?**

**6. Data Link Layer — Local Network**

Wi-Fi or Ethernet carries frames across the local network link.

Layer 2 · Frames and MAC addresses

**Which layer do cables work in OSI?**

**7. Physical Layer — Signals**

The data travels as radio signals over Wi-Fi or as electrical or optical signals through the network.

Layer 1 · Bits and signals

---

### TCP/IP Model — WhatsApp Story 📱

Imagine a student sends “Hello, Sir!” to a teacher on WhatsApp. How does the message travel through the internet?

**4**

**Layer — Application Layer, Presentation Layer, Session Layer**

**Application Layer**

The student types “Hello, Sir!” in WhatsApp. Application protocols provide network services to the app.

Examples: HTTP, DNS, SMTP

**3**

**Layer — Transport Layer**

**Transport Layer**

TCP or UDP transports data between endpoints. TCP provides reliable, ordered delivery; UDP does not provide those guarantees by itself.

Examples: TCP, UDP

**2**

**Layer — Network Layer**

**Internet Layer**

IP addresses and routers help packets travel across networks toward the teacher's device.

Examples: IPv4, IPv6, ICMP

**1**

**Layer — Data Link Layer, Physical Layer**

**Network Access Layer**

Wi-Fi or Ethernet carries the data over the local network as signals and frames.

Examples: Wi-Fi, Ethernet



## Transport Layer — TCP and UDP

The Transport Layer has two main types of protocols:

1. TCP (Transmission Control Protocol)
2. UDP (User Datagram Protocol)

---

### 1. TCP (Transmission Control Protocol)

TCP works using a client-server model. It provides reliable data delivery between applications.

#### TCP 3-Way Handshake

Before transferring data, TCP establishes a connection between the client and the server.

**Step 1: SYN**

The client sends a SYN packet to the server to request a connection.

**Step 2: SYN-ACK**

The server sends a SYN-ACK packet back to the client to acknowledge the request and synchronize sequence numbers.

**Step 3: ACK**

The client sends an ACK packet to the server.

Now, the TCP connection is established, and data transfer can begin.

#### TCP 3-Way Handshake Diagram

```text
        CLIENT                              SERVER
           |                                   |
           | -------- SYN -------------------> |
           |                                   |
           | <------ SYN + ACK --------------- |
           |                                   |
           | -------- ACK -------------------> |
           |                                   |
           |       Connection Established      |
           |                                   |
           | <====== Data Transfer ==========> |
```

### Why Do We Use TCP?

TCP provides reliable data delivery. It detects lost data and retransmits it when necessary, and it ensures that data is delivered in order to the receiving application.

For example, when you send an email through Gmail, losing part of the message would be a problem. TCP helps provide reliable delivery of the data between network endpoints.

### Protocols That Commonly Use TCP

**1. HTTP (Hypertext Transfer Protocol)**

HTTP is used to transfer web content between a client and a server. HTTP can use TCP.

**2. HTTPS (Hypertext Transfer Protocol Secure)**

HTTPS secures web communication using TLS. Traditional HTTP/1.1 and HTTP/2 over HTTPS commonly use TCP.

**3. SMTP (Simple Mail Transfer Protocol)**

SMTP is used to send and relay emails between mail clients and mail servers or between mail servers.

For example, when you send an email saying "Hello, Sir!", SMTP can be used to send the email, while TCP provides reliable transport for the SMTP connection.

**4. SSH (Secure Shell)**

SSH is used to securely connect to and manage remote computers or servers. SSH commonly uses TCP.

For example, a DevOps engineer can use SSH to connect to an AWS EC2 instance and manage it remotely.

SSH commonly runs in the background of a terminal session while the engineer executes commands on the remote server.

---

### 2. UDP (User Datagram Protocol)

UDP is another Transport Layer protocol. It allows applications to send data without establishing a connection first.

Unlike TCP, UDP does not guarantee that packets will arrive, arrive in order, or be retransmitted if lost.

#### How UDP Works

- The client sends data to the server.
- The server can receive the data without a TCP-style handshake.
- Some packets may get lost during transmission.
- UDP itself does not retransmit lost packets or guarantee delivery.

Applications can implement their own reliability mechanisms if required.

### What Happens When UDP Packets Are Lost?

For example, imagine you are playing an online game.

If a small update about a player's position is lost, the game may simply use the next update instead of waiting for the old one.

UDP can be useful for real-time applications because avoiding delays may be more important than retransmitting every lost packet.

### UDP Examples

- Online gaming
- Live audio and video
- Real-time communication
- DNS queries in many common configurations

### Bandwidth, Latency, and Packet Loss

**Bandwidth:** The amount of data a network can carry per second.

**Latency:** The time it takes for data to travel from one endpoint to another.

**Packet loss:** When data packets fail to reach their destination.

Packet loss can affect both TCP and UDP. TCP may retransmit lost data, which can increase delays and network traffic. UDP does not retransmit lost packets by itself, so applications may experience missing data.

Using more bandwidth does not automatically increase latency. However, network congestion can increase latency and packet loss.

---

### TCP vs UDP

| Feature | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented | Connectionless |
| Handshake | 3-way handshake | No TCP-style handshake |
| Reliability | Reliable delivery | No delivery guarantee by itself |
| Packet ordering | Ordered delivery | No ordering guarantee |
| Retransmission | Handles retransmission | No retransmission by itself |
| Examples | HTTP/1.1, HTTP/2, SMTP, SSH | Online gaming, real-time media, DNS |

### Quick Revision

- **TCP:** Reliable and ordered data delivery.
- **UDP:** Sends data without establishing a connection first.
- **SYN:** Client requests a TCP connection.
- **SYN-ACK:** Server acknowledges the request and responds.
- **ACK:** Client acknowledges the server's response.
- **SMTP:** Sends and relays emails.
- **SSH:** Securely connects to remote servers.
- **Latency:** Time taken for data to travel.
- **Packet loss:** Data packets that fail to reach their destination.


## 4. How Does Security Work on the Internet?

### 1. Firewall

A firewall controls incoming and outgoing network traffic based on security rules.

For example, when we launch an Ubuntu server on AWS, the server may have a public IP address. However, having a public IP does not mean everyone can access every service running on the server.

The firewall or AWS Security Group controls which traffic is allowed to reach the server.

### 2. Ingress and Egress Traffic

There are two types of traffic directions:

**Ingress (Inbound) Traffic**

Ingress means incoming traffic that enters the server or network.

Example:
- A client sends a request to access a website.
- The request travels through the internet toward the server.
- The server's security rules determine whether the request is allowed.

**Egress (Outbound) Traffic**

Egress means outgoing traffic that leaves the server or network.

Example:
- An Ubuntu server downloads Nginx packages from the internet.
- The server sends outgoing requests to package repositories.
- Its outbound security rules determine which traffic is allowed.

**Traffic means data moving across a network**, such as requests, responses, and packets.

### 3. IP Address and Network Layer

At the Network Layer (Layer 3 of the OSI model), IP addresses help identify the source and destination of packets and route them across networks.

For example, when you access a website using a server's public IP address, your request needs to reach the correct destination.

However, an IP address alone does not guarantee access. Network routes, firewall rules, and the application service must also be configured correctly.

---

### 4. Practical Example — Install Nginx on an Ubuntu Server

Suppose you launch an Ubuntu EC2 instance on AWS and install Nginx.

**Step 1: Install Nginx**

```bash
sudo apt-get update
sudo apt-get install nginx
```

**Step 2: Start Nginx**

```bash
sudo systemctl start nginx
```

Check whether Nginx is running:

```bash
sudo systemctl status nginx
```

**Step 3: Open the Server's Public IP Address**

Open your browser and enter:

```text
http://YOUR_PUBLIC_IP
```

You may see the error:

```text
This site can't be reached
```

### Why Does This Happen?

Nginx may be installed and running correctly, but the AWS Security Group might not allow incoming HTTP traffic on port 80.

The request needs permission to reach the web server.

---

### 5. AWS Security Group Rules

An AWS Security Group acts as a virtual firewall for an EC2 instance.

It contains inbound and outbound rules.

#### Inbound Rules

Inbound rules control traffic coming into the EC2 instance.

| Type | Protocol | Port | Purpose |
|---|---|---|---|
| SSH | TCP | 22 | Remote server access |
| HTTP | TCP | 80 | Website access |
| HTTPS | TCP | 443 | Secure website access |

**Important:** Port 22 is used for SSH, not for website access. To access the default Nginx webpage over HTTP, allow inbound TCP traffic on port 80.

#### Outbound Rules

Outbound rules control traffic leaving the EC2 instance.

A default Security Group configuration commonly allows all outbound traffic.

For example, Ubuntu may need outbound access to download software packages using `apt`.

Outbound rules can be restricted when required, but doing so may prevent package downloads or other services from working.

---

### 6. Configure Inbound Rules in AWS

Follow these steps:

1. Open the AWS Management Console.
2. Go to **EC2 → Instances**.
3. Select your Ubuntu instance.
4. Open the **Security** tab.
5. Click the associated Security Group.
6. Select **Edit inbound rules**.
7. Add an HTTP rule:
   - Type: HTTP
   - Protocol: TCP
   - Port range: 80
   - Source: Choose an appropriate IPv4 source range.
8. Save the rules.

Now open the public IP address in your browser using HTTP.

```text
http://YOUR_PUBLIC_IP
```

If Nginx is running and the network configuration is correct, the Nginx welcome page should appear.

### 7. What Does 0.0.0.0/0 Mean?

`0.0.0.0/0` means all IPv4 addresses.

If you configure an inbound rule with this source, traffic from any IPv4 address can attempt to reach that port, subject to other network controls.

For example:

- HTTP port 80 with source `0.0.0.0/0`: the website can be publicly accessible.
- SSH port 22 with source `0.0.0.0/0`: SSH access is exposed to all IPv4 addresses, which is generally unsafe.

### 8. What Does My IP /32 Mean?

`/32` represents a single IPv4 address.

For example:

```text
203.0.113.25/32
```

This CIDR notation represents one IPv4 address.

When configuring SSH access, choose **My IP** in the AWS console to restrict access to your current public IPv4 address.

This is safer than allowing SSH access from anywhere. If your public IP changes, you may need to update the rule.

### 9. Important Security Best Practices

- Allow SSH (port 22) only from trusted IP addresses.
- Allow HTTP (port 80) publicly only when the website is intended to be public.
- Use HTTPS (port 443) for secure website communication.
- Avoid opening unnecessary ports.
- Remember that a public IP does not automatically make a service accessible.
- Check the Security Group, network ACLs, routing, server firewall, and service status when troubleshooting access problems.

### Quick Revision

- **Firewall:** Controls network traffic using security rules.
- **Ingress:** Incoming traffic.
- **Egress:** Outgoing traffic.
- **IP address:** Identifies a network endpoint for IP communication.
- **Port 22:** SSH.
- **Port 80:** HTTP.
- **Port 443:** HTTPS.
- **0.0.0.0/0:** All IPv4 addresses.
- **/32:** One IPv4 address.
- **AWS Security Group:** Controls inbound and outbound traffic for AWS resources.

## TLS Certificate and UFW Firewall

### 1. TLS Certificate

TLS stands for **Transport Layer Security**.

TLS helps secure communication between a client and a server by encrypting data during transmission.

For example, when you open an HTTPS website, TLS helps protect the data exchanged between your browser and the website.

- HTTP uses port 80 by default.
- HTTPS commonly uses port 443.
- TLS helps provide encryption, authentication, and data integrity.

### 2. UFW (Uncomplicated Firewall)

UFW is a firewall management tool commonly used on Ubuntu Linux.

It allows us to control incoming and outgoing network traffic using firewall rules.

**Check UFW status:**

```bash
sudo ufw status
```

**Enable UFW:**

```bash
sudo ufw enable
```

**Allow SSH:**

```bash
sudo ufw allow 22/tcp
```

**Allow HTTP:**

```bash
sudo ufw allow 80/tcp
```

**Allow HTTPS:**

```bash
sudo ufw allow 443/tcp
```

**Allow a specific port:**

```bash
sudo ufw allow 8080/tcp
```

### 3. Delete a Particular UFW Rule

If you want to delete a particular firewall rule, first check the numbered rules.

```bash
sudo ufw status numbered
```

Example output:

```text
[ 1] 22/tcp    ALLOW IN    Anywhere
[ 2] 80/tcp    ALLOW IN    Anywhere
[ 3] 443/tcp   ALLOW IN    Anywhere
```

Suppose you want to delete the HTTP rule on port 80.

**Step 1: Delete the rule by number**

```bash
sudo ufw delete 2
```

This deletes rule number 2 in the displayed list.

**Important:** Rule numbers can change after a rule is deleted. Check the numbered list again before deleting another rule.

**Alternative: Delete by rule definition**

```bash
sudo ufw delete allow 80/tcp
```

This removes the matching allow rule for TCP port 80.

### Quick Revision

- **TLS:** Secures communication using encryption and authentication.
- **HTTPS:** HTTP secured using TLS.
- **UFW:** Ubuntu firewall management tool.
- **ufw allow:** Adds a firewall rule.
- **ufw status numbered:** Displays firewall rules with numbers.
- **ufw delete:** Removes a firewall rule.
- If you are connected to a remote Ubuntu or AWS EC2 server over SSH, allow SSH before enabling UFW:
sudo ufw allow 22/tcp
sudo ufw enable

# 5. Network Security and AWS VPC

## 1. Three Important Things in Network Communication

For network communication, three important things are:

1. Protocol
2. IP Address
3. Port Number

### Daily-Life Example: Sending a Letter

Imagine you want to send a letter to your friend.

- **IP Address:** Your friend's house address tells the postal service where to deliver the letter.
- **Port Number:** Imagine your friend lives in an apartment building. The apartment number identifies the correct destination inside the building.
- **Protocol:** The rules followed by the postal service are similar to communication protocols.

In networking, these three concepts help data reach the correct destination and service.

### Protocol

A protocol defines the rules for communication between devices.

Examples:
- HTTP — Transfers web content.
- HTTPS — Transfers web content securely using TLS.
- SSH — Securely connects to remote servers.
- TCP — Provides reliable, ordered data delivery.
- UDP — Sends data without establishing a connection first.

### IP Address

An IP address identifies a network endpoint and helps route data packets across networks.

Example:

`192.168.1.10`

Daily-life example: An IP address is like a house address used to find the destination.

### Port Number

A port number identifies the application or service receiving network traffic on a device.

Examples:

| Port | Service | Purpose |
|---|---|---|
| 22 | SSH | Remote server access |
| 80 | HTTP | Website access |
| 443 | HTTPS | Secure website access |

Daily-life example: If the IP address is the building address, the port is like the apartment number for the intended service.

**Remember:** The IP address helps identify the destination, the port identifies the service, and the protocol defines how communication happens.

---

## 2. What Is a Firewall?

A firewall controls incoming and outgoing network traffic according to security rules.

Daily-life example: A security guard at a building checks who is allowed to enter and who is allowed to leave.

In networking:

- **Ingress (Inbound):** Traffic coming into a server or network.
- **Egress (Outbound):** Traffic leaving a server or network.

For example, when a user opens your website, the incoming request is ingress traffic. When your Ubuntu server downloads an update, that request is egress traffic.

A firewall can allow or block traffic based on configured rules.

---

## 3. What Is a VPC in AWS?

VPC stands for **Virtual Private Cloud**.

A VPC is a logically isolated virtual network in AWS where we can launch resources such as EC2 instances.

Inside one VPC, we can create multiple subnets.

For example:
- Public subnet
- Private subnet

### Daily-Life Example: A Gated Society

Imagine a gated society with different areas:

- The main gate connects the society to the outside world.
- The reception area is accessible to visitors.
- Private residential areas are restricted to authorized people.
- Internal roads connect different buildings.

Similarly, in AWS:

- **VPC:** The entire gated society.
- **Public subnet:** An area designed for resources that need internet connectivity.
- **Private subnet:** An area for resources that should not be directly accessible from the public internet.
- **Route table:** The directions that determine where traffic should go.
- **Security Group:** A virtual security guard controlling permitted traffic.

---

## 4. Public Subnet

A public subnet has a route to an Internet Gateway.

It is commonly used for resources that need to receive public internet traffic.

Examples:
- Public-facing web servers
- Internet-facing load balancers
- Bastion hosts

For an EC2 instance to be directly accessible from the internet, it also needs an appropriate public IP address and security rules allowing the required traffic.

### Daily-Life Example

A shop located at the entrance of a society is easy for visitors to reach.

Similarly, a public-facing web server can receive requests from internet users when its network and security settings permit access.

---

## 5. Private Subnet

A private subnet is generally used for resources that should not be directly accessible from the public internet.

Examples:
- Application servers
- Databases
- Internal services

### Daily-Life Example

Imagine a society's private residential area. Visitors cannot directly enter it from the street without the appropriate access.

Similarly, private EC2 instances are not directly reachable from the public internet through a normal inbound internet route.

Private resources can still communicate with other permitted resources inside the VPC.

They may also access the internet for outbound connections through a NAT Gateway.

---

## 6. Internet Gateway (IGW)

An Internet Gateway connects a VPC to the internet when the network is configured correctly.

### Daily-Life Example

The main gate of a society connects the society's internal roads to the outside road.

Similarly, an Internet Gateway allows appropriately configured VPC resources to communicate with the internet.

### How Does It Work?

Suppose you launch an Ubuntu EC2 instance and install Nginx.

First, install Nginx:

```bash
sudo apt-get update
sudo apt-get install nginx
```

Start Nginx:

```bash
sudo systemctl start nginx
```

Check its status:

```bash
sudo systemctl status nginx
```

Now open your EC2 instance's public IP address in a browser:

```text
http://YOUR_PUBLIC_IP
```

If you see "This site can't be reached," one possible reason is that inbound HTTP traffic is not allowed by the AWS Security Group.

For the website to work, check:
- The instance has a suitable public IP address.
- The subnet route table has a route to the Internet Gateway.
- The Security Group allows inbound TCP port 80.
- The operating system firewall permits the traffic.
- Nginx is running and listening on the correct port.

### HTTP Inbound Rule

In AWS, open:

EC2 → Instances → Select Instance → Security → Security Group → Edit inbound rules.

Add:

| Setting | Value |
|---|---|
| Type | HTTP |
| Protocol | TCP |
| Port | 80 |
| Source | `0.0.0.0/0` for a publicly accessible website |

`0.0.0.0/0` means all IPv4 addresses. Use it only when public access is intended.

---

## 7. NAT Gateway

NAT stands for Network Address Translation.

A NAT Gateway allows resources in a private subnet to initiate connections to the internet without allowing unsolicited inbound internet connections through that gateway.

### Daily-Life Example

Imagine a resident in a private residential area wants to order something from an outside shop.

The resident makes the request through an authorized common service. The outside shop responds through that service, but it cannot automatically enter the resident's private home.

Similarly, a private EC2 instance can download updates or software from the internet through a NAT Gateway.

### How Does NAT Gateway Work?

Suppose an EC2 instance in a private subnet needs to download software updates.

The traffic follows this path:

```text
Private EC2 Instance
        |
        v
Private Subnet Route Table
        |
        v
NAT Gateway
(Public Subnet)
        |
        v
Internet Gateway
        |
        v
Internet
```

Steps:

1. The private EC2 instance sends an outbound request.
2. Its route table directs internet-bound traffic to the NAT Gateway.
3. The NAT Gateway translates the source address.
4. Traffic leaves the VPC through the Internet Gateway.
5. The response returns through the NAT Gateway to the private instance.

**Important:** A NAT Gateway does not provide direct inbound internet access to the private EC2 instance.

---

## 8. CIDR — IP Address Range

CIDR stands for **Classless Inter-Domain Routing**.

CIDR notation defines an IP address range for a network or subnet.

Example:

`10.0.0.0/16`

This IPv4 CIDR block contains 65,536 addresses.

### Daily-Life Example: Dividing a Society Into Blocks

Imagine a large society with many houses.

You divide it into smaller blocks:
- Block A
- Block B
- Block C

Each block contains a specific range of house numbers.

Similarly, CIDR allows us to divide a large IP address range into smaller subnet ranges.

### Example AWS VPC

```text
VPC: 10.0.0.0/16
       |
       |---- Public Subnet:  10.0.1.0/24
       |
       |---- Private Subnet: 10.0.2.0/24
```

- `10.0.0.0/16` is the VPC address range.
- `10.0.1.0/24` is the public subnet range.
- `10.0.2.0/24` is the private subnet range.

Each `/24` contains 256 total IPv4 addresses. AWS reserves five addresses in each IPv4 subnet, leaving 251 available for resources.

### Why Do We Use CIDR?

- To define the IP range of a VPC.
- To divide a VPC into multiple subnets.
- To allocate addresses to network resources.
- To organize and manage network routing.

---

## 9. Complete AWS VPC Architecture

```text
                       INTERNET
                           |
                           v
                  INTERNET GATEWAY
                           |
               +-----------+-----------+
               |                       |
               v                       v
         PUBLIC SUBNET            PUBLIC SUBNET
         10.0.1.0/24               10.0.3.0/24
               |                       |
          Web Server              NAT Gateway
                                       |
                                       v
                                PRIVATE SUBNET
                                 10.0.2.0/24
                                       |
                                App / Database
```

This is a simplified architecture.

- The public web server receives permitted user requests.
- The NAT Gateway allows private resources to initiate outbound internet connections.
- The private application or database resources are not directly exposed to the public internet through a normal inbound route.
- Route tables determine where traffic goes.
- Security Groups control which traffic is permitted.

For production systems, resources are commonly distributed across multiple Availability Zones to improve availability and resilience.

---

## 10. Quick Revision

| Concept | Simple Meaning | Daily-Life Example |
|---|---|---|
| Protocol | Rules for communication | Postal delivery rules |
| IP Address | Identifies a network destination | House address |
| Port | Identifies an application or service | Apartment number |
| Firewall | Controls network traffic | Security guard |
| VPC | Isolated virtual network | Gated society |
| Public Subnet | Subnet with a route to an Internet Gateway | Public-facing shop |
| Private Subnet | Subnet for internal resources | Restricted residential area |
| Internet Gateway | Connects a VPC to the internet | Main gate |
| NAT Gateway | Enables private resources to initiate outbound internet connections | Authorized common service |
| CIDR | Defines an IP address range | Dividing houses into blocks |
| Route Table | Directs network traffic | Road directions |
| Security Group | Allows or blocks traffic to resources | Entry permission rules |
