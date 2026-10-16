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
