---
layout: post
title: "Welcome to CyberJournalLogs! With JAM"
date: 2025-07-05
categories: cyberjournallogs getting-started
tags: [first-post, cyberjournallogs, OSI Understanding, Advanced Level]
---

**OPEN SYSTEM INTERCONNECTION** 

OSI Layer Understanding: 
OSI is a framework that standardizes the functions of telecommunication or computing systems into seven layers. Each layer has specific responsibilities. With this flow, we can understand how communication works and which security layers it passes through. 
Let's see from my perspective now.

---

<p align="center">
  <img src="https://wearejam.github.io/cyberjournallogs/osi_architecture_diagram_1.pdf_20250729_121353_0000.pdf" alt="OSI Diagram 1">
</p>

---

The above image shows the flow of communication reaching from sender A to receiver B.  
Let's see how I picture this OSI layer. This sender A communication will always encrypt the message, and receiver B will decrypt the data. 

Let's see this OSI layer with an example: Email

---

<p align="center">
  <img src="https://wearejam.github.io/cyberjournallogs/assets/images/OSI2.png" alt="OSI Diagram 2">
</p>

---

**Sender's Side:  Encryption process** 

1. Application Layer - The user composes and sends an email using an application like Gmail or Outlook. The app uses SMTP (Simple Mail Transfer Protocol) to handle the message.It sends the raw data (email) down to the next layer as an APDU (Application Protocol Data Unit).

2. Presentation layer - The Presentation Layer is responsible for formatting, compressing, or encrypting data.In this case, it encrypts the raw email using TLS (Transport Layer Security).
The result is passed to the session layer as a PPDU (Presentation PDU).

3. Session Layer -  This layer sets up and manages the session (start → manage → end) between sender and receiver. It maintains dialog and synchronizes communication.It forwards the encrypted data with session control info to the transport layer as an SPDU (Session PDU)

4. Transport Layer - The encrypted data is split into smaller chunks, called segments.Each segment gets a TCP header (if using TCP), containing:
   -> Source and destination port numbers
   -> Sequence and acknowledgment numbers
Every segment becomes a TPDU (Transport PDU).These TPDUs are handed to the Network Layer.

5. Network Layer - Each TPDU is wrapped in an IP packet with:
   -> Source IP address (e.g., your device)
   -> Destination IP address (e.g., Gmail server)
These are now Packets (Network Layer PDUs).Packets are forwarded to the next layer.

6. Data Link Layer - The IP packet is encapsulated inside a frame with:
   -> MAC address of the next-hop router (or local device)
   -> Frame Check Sequence (FCS) for error detection
This becomes a Frame (Data Link PDU). Sent to the physical layer.

7. Physical Layer - The frame is turned into raw bits (1s and 0s). These bits are sent as electrical, optical, or radio signals through the physical medium (like Ethernet cable, Wi-Fi, or fiber).
Devices used: NICs, hubs, cables, repeaters, antennas, etc.

**Receiver’s Side: Decryption process**

Now the receiver side 

8. Physical Layer - Bits are reassembled into frames 

9. Data Link Layer - MAC checked

10. Network Layer - IP checked

11. Transport Layer - Segments are reordered and checked

12. Session Layer - Session validated

13. Presentation Layer - Email decrypted
    
14. Application Layer - Email gets to the Inbox 


----- Jamming With JAM -----
