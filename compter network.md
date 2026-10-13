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
