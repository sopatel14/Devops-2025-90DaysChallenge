#Week1 - Networking


# 🚀 Starting My DevOps Journey: Understanding Networking Fundamentals with "Train With Shubham"

As I begin my DevOps journey, I’ve decided to start with something foundational — **Networking**. Inspired and guided by [Train With Shubham](https://github.com/trainwithshubham), I explored how the internet works, studied essential models like OSI and TCP/IP, and practiced hands-on tasks like launching AWS EC2 instances and using networking commands.

Here’s a summary of what I’ve learned so far, along with a few beginner tasks I’ve completed.

---

## 🌐 How Does the Internet Work?

The internet is essentially a vast network of **optical fiber cables** connecting the world — including deep-sea cables that run under the oceans. These cables transmit data across massive distances in milliseconds.

Every time you open a website or send a message, it travels through a complex system of routers, switches, and servers. Pretty wild when you think about the journey your data takes!

---

## 🖧 Types of Networks

| Type    | Full Form                 | Usage                                        |
| ------- | ------------------------- | -------------------------------------------- |
| **WAN** | Wide Area Network         | Connects networks over a country or globally |
| **MAN** | Metropolitan Area Network | Used in a city-wide setup                    |
| **LAN** | Local Area Network        | Used in homes, schools, or offices           |
| **PAN** | Personal Area Network     | Bluetooth or mobile hotspot connections      |

---

## 📊 OSI Model – Understanding Data Transmission

The **OSI (Open Systems Interconnection)** model isn’t directly used in real-world networking, but it’s a great conceptual tool to understand **how data flows** through a system.

**7 Layers of OSI Model:**

1. **Application Layer** – User-facing software like web browsers
2. **Presentation Layer** – Formats and encrypts data
3. **Session Layer** – Maintains sessions between devices
4. **Transport Layer** – Splits data into segments (TCP)
5. **Network Layer** – Adds IP address and routing
6. **Data Link Layer** – Frames the data for transmission
7. **Physical Layer** – Actual physical transmission (cables, signals)

When data is sent, it goes **down through the 7 layers** from sender to receiver and then **back up the layers** on the receiving device.

---

## 📦 TCP/IP Model – Real-World Networking

The **TCP/IP model** is what the internet actually uses. It’s a simplified and practical model with just **4 layers**:

1. **Application Layer** – Where protocols like HTTP, FTP, SSH live
2. **Transport Layer** – Manages data delivery using TCP/UDP
3. **Internet Layer** – Adds IP addresses and routes packets
4. **Network Access Layer** – Sends/receives data over the physical medium

### ⚡ Why is TCP/IP Preferred?

* It’s simpler than OSI
* It’s actually used in all real-world networks
* It directly maps to internet protocols

---

## 🔢 IP Address vs MAC Address

| Type            | What It Does                                                                          |
| --------------- | ------------------------------------------------------------------------------------- |
| **IP Address**  | A logical address assigned by the network. It helps locate devices on the internet.   |
| **MAC Address** | A permanent hardware ID assigned to your network adapter. It’s unique to each device. |

Both are essential for identifying and communicating with devices in a network.

---

## 🔌 Routers vs Switches

| Device     | Role                                                                         |
| ---------- | ---------------------------------------------------------------------------- |
| **Router** | Connects different networks (e.g., your home network to the internet)        |
| **Switch** | Connects multiple devices within a single network (e.g., computers in a LAN) |

---

## 🔐 Common Network Protocols Every DevOps Engineer Should Know

| Protocol  | Port | Use Case                       |
| --------- | ---- | ------------------------------ |
| **HTTP**  | 80   | Insecure web browsing          |
| **HTTPS** | 443  | Secure web browsing            |
| **FTP**   | 21   | File transfers                 |
| **SSH**   | 22   | Secure shell access to servers |
| **DNS**   | 53   | Resolves domain names to IPs   |

These protocols are frequently used in DevOps workflows — whether you’re configuring web servers, automating deployments, or troubleshooting issues.

---

## ☁️ AWS EC2 & Security Groups – Quick Setup Guide

I also got hands-on with **AWS EC2**, learning how to create and secure a cloud instance.

### ✅ How to Launch an EC2 Instance:

1. Go to the **EC2 Dashboard** on AWS.
2. Click on **Launch Instance**.
3. Choose **Amazon Linux 2 (Free Tier)**.
4. Select instance type: **t2.micro** (Free Tier).
5. Configure instance settings (default is fine).
6. Under **Security Groups**:

   * Create a new one with rules for ports:

     * `22` (SSH)
     * `80` (HTTP)
     * `443` (HTTPS)
7. Launch the instance and download the `.pem` key pair.
8. Connect using SSH:

   ```bash
   ssh -i "your-key.pem" ec2-user@<your-ec2-public-ip>
   ```

> **Security Groups** are like firewalls. They define what type of traffic is allowed in/out of your EC2 instance. Super important for cloud security!

---

## 🔧 Networking Commands – A Handy Cheat Sheet

Here are some basic networking commands I practiced:

| Command                  | Purpose                       | Example                                                         |
| ------------------------ | ----------------------------- | --------------------------------------------------------------- |
| `ping`                   | Test connectivity             | `ping google.com`                                               |
| `traceroute` / `tracert` | Trace route of packets        | `traceroute google.com` (Linux), `tracert google.com` (Windows) |
| `netstat`                | View open network connections | `netstat -an`                                                   |
| `curl`                   | Make HTTP requests            | `curl https://example.com`                                      |
| `dig` / `nslookup`       | DNS resolution                | `dig google.com` / `nslookup google.com`                        |

These are essential tools for DevOps professionals to **debug**, **verify connectivity**, and **troubleshoot DNS issues**.

---

## 🙌 Final Thoughts

This was just the beginning, but understanding networking is like learning the language of the internet — and it's absolutely critical for anyone in DevOps.

Big thanks to **Train With Shubham** for the guidance and structured challenges. Next up: diving deeper into **Linux fundamentals** and **Cloud Infrastructure**!

---

If you’re starting your DevOps journey too, feel free to connect and share your learning! Let’s grow together. 💪

---

**#DevOps #Networking #AWS #TrainWithShubham #BeginnerBlog #OSIModel #TCPIP #EC2 #SecurityGroups #Linux #DevOpsJourney**

