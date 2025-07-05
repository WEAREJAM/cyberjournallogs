---
layout: post
title: "Welcome to CyberJournalLogs! With JAM"
date: 2025-07-05
categories: cyberjournallogs getting-started
tags: [first-post, cyberjournallogs, OSI Understanding, Advanced Level]
---
OPEN SYSTEM INTERCONNECTION 

OSI Layer Understanding: 
OSI is a framework that standardizes the functions of telecommunication or computing systems into seven layers. Each layer has specific responsibilities. With this flow, we can understand how communication works and which security layers it passes through. 

Let's see from my perspective now.
---

<p align="center">
  <img src="assets/images/OSI1.png" alt="OSI Banner" width="500">
</p>

---
The above image shows the flow of communication reaching from sender A to receiver B. 
Let's see how I picture this OSI layer. This sender A communication will always encrypt the message, and receiver B will decrypt the data. 

Let's see this OSI layer with an example: Email 
---

<p align="center">
  <img src="assets/images/OSI2.png" alt="OSI Banner" width="500">
</p>

---

**Sender's Side:  Encryption process** 

Application Layer - The user composes and sends an email using an application like Gmail or Outlook. The app uses SMTP (Simple Mail Transfer Protocol) to handle the message.It sends the raw data (email) down to the next layer as an APDU (Application Protocol Data Unit).

Presentation layer - The Presentation Layer is responsible for formatting, compressing, or encrypting data.In this case, it encrypts the raw email using TLS (Transport Layer Security).
The result is passed to the session layer as a PPDU (Presentation PDU).

Session Layer -  This layer sets up and manages the session (start → manage → end) between sender and receiver. It maintains dialog and synchronizes communication.It forwards the encrypted data with session control info to the transport layer as an SPDU (Session PDU)

Transport Layer - The encrypted data is split into smaller chunks, called segments.Each segment gets a TCP header (if using TCP), containing:
1. Source and destination port numbers
2. Sequence and acknowledgment numbers
Every segment becomes a TPDU (Transport PDU).These TPDUs are handed to the Network Layer.

Network Layer - Each TPDU is wrapped in an IP packet with:
1. Source IP address (e.g., your device)
2. Destination IP address (e.g., Gmail server)
These are now Packets (Network Layer PDUs).Packets are forwarded to the next layer.

Data Link Layer - The IP packet is encapsulated inside a frame with:
1. MAC address of the next-hop router (or local device)
2. Frame Check Sequence (FCS) for error detection
This becomes a Frame (Data Link PDU). Sent to the physical layer.

Physical Layer - The frame is turned into raw bits (1s and 0s). These bits are sent as electrical, optical, or radio signals through the physical medium (like Ethernet cable, Wi-Fi, or fiber).
Devices used: NICs, hubs, cables, repeaters, antennas, etc.

**Receiver’s Side: Decryption process**

Now the receiver side 
Physical Layer - Bits are reassembled into frames 
Data Link Layer - MAC checked
Network Layer - IP checked
Transport Layer - Segments are reordered and checked
Session Layer - Session validated
Presentation Layer - Email decrypted 
Application Layer - Email gets to the Inbox 



