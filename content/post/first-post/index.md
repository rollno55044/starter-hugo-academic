---
title: Transport layer
subtitle: This is part of series on networking for system design  caution — aim
  of these series is not to make you networking expert. this is just prepare you
  for system design
date: 2023-02-11T11:48:05.967Z
summary: >-
  This is part of series on networking for system design  


  caution — aim of these series is not to make you networking expert. this is just prepare you for system design
draft: false
featured: false
tags:
  - System Design
categories:
  - System Design
image:
  filename: ""
  focal_point: Smart
  preview_only: true
  alt_text: "**Caution** — Aim of these series is not to make you networking
    expert. this is just prepare you for system design"
---
**Caution** — Aim of these series is not to make you networking expert. this is just prepare you for system design

The transport layer is responsible for lots of important functions of reliable computer networking. These include multiplexing and demultiplexing traffic, establishing long running connections and ensuring data integrity through error checking and data verification

![](https://miro.medium.com/max/1400/1*5M-PBCOgHAQfa3iWqpNIeA.png)



﻿**[Control](https://en.wikipedia.org/wiki/Flow_control_%28data%29)**: The rate of data transmission between two nodes must sometimes be managed to prevent a fast sender from transmitting more data than can be supported by the receiving [data buffer](https://en.wikipedia.org/wiki/Data_buffer), causing a buffer overrun. This can also be used to improve efficiency by reducing [buffer underrun](https://en.wikipedia.org/wiki/Buffer_underrun).

**[Congestion avoidance](https://en.wikipedia.org/wiki/Congestion_avoidance):** [Congestion control](https://en.wikipedia.org/wiki/Congestion_control) can control traffic entry into a telecommunications network, so as to avoid [congestive collapse](https://en.wikipedia.org/wiki/Congestive_collapse) by attempting to avoid oversubscription of any of the processing or [link](https://en.wikipedia.org/wiki/Data_link)capabilities of the intermediate nodes and networks and taking resource reducing steps, such as reducing the rate of sending [packets](https://en.wikipedia.org/wiki/Packet_%28information_technology%29). For example, [automatic repeat requests](https://en.wikipedia.org/wiki/Automatic_repeat_request) may keep the network in a congested state; this situation can be avoided by adding congestion avoidance to the flow control, including [slow-start](https://en.wikipedia.org/wiki/Slow-start). This keeps the bandwidth consumption at a low level in the beginning of the transmission, or after packet retransmission.

**MULTIPLEXING**: [Ports](https://en.wikipedia.org/wiki/TCP_and_UDP_port) can provide multiple endpoints on a single node. For example, the name on a postal address is a kind of multiplexing, and distinguishes between different recipients of the same location. Computer applications will each listen for information on their own ports, which enables the use of more than one [network service](https://en.wikipedia.org/wiki/Network_service) at the same time. It is part of the transport layer in the [TCP/IP model](https://en.wikipedia.org/wiki/TCP/IP_model), but of the [session layer](https://en.wikipedia.org/wiki/Session_layer) in the OSI model.

![](https://miro.medium.com/max/1400/1*PUMJJcUgeauRCdYQoYlsRA.png)

**PORT** :- A port is a 16-bit number that’s used to direct traffic to specific services running on a networked computer.

![](https://miro.medium.com/max/1400/1*52fDu3__9kGKycUTH8s09A.png)

There are two types of connection at transport layer -

**CONNECTION-ORIENTED PROTOCOL** — A connection-oriented protocol is one that establishes a connection, and uses this to ensure that all data has been properly transmitted. A connection at the transport layer implies that every segment of data sent is acknowledged. This way, both ends of the connection always know which bits of data have definitely been delivered to the other side and which haven’t. Connection-oriented protocols are important because the Internet is a vast and busy place, and lots of things could go wrong while trying to get data from point A to point B. Example — TCP

CONNECTION LESS PROTOCOL — no three way handshake , no four way handshake . Just send the data and pray ………… Example — UDP

**”TCP “ —** —

***TCP SEGMENT : —***

![](https://miro.medium.com/max/1400/1*RF1F6Mdz_EVbVbSSwYj-GQ.jpeg)

First, we have the **source port and the destination port fields.** The destination port is the port of the service the traffic is intended for, source port is required to keep lots of outgoing connections separate. You know how a destination port, say port 80, is needed to make sure traffic reaches a web server running on a certain IP? Similarly, a source port is needed so that when the web server replies, the computer making the original request can send this data to the program that was actually requesting it. It is in this way that when it web server responds to your requests to view a webpage that this response get received by your web browser and not your word processor.

Next up is a field known as the **sequence number**. This is a 32-bit number that’s used to keep track of where in a sequence of TCP segments this one is expected to be. At the transport layer, TCP splits all of this data up into many segments. The sequence number in a header is used to keep track of which segment out of many this particular segment might be. The next field, the acknowledgment number, is a lot like the sequence number.

The **acknowledgment number** is the number of the next expected segment. In very simple language, a sequence number of one and an acknowledgement number of two could be read as this is segment one, expect segment two next.

**data offset —** — This field is a four-bit number that communicates how long the TCP header for this segment is. This is so that the receiving network device understands where the actual data payload begins..Then, we have six bits that are reserved for the six TCP control flags.

The next field is a 16-bit **TCP window.** — A TCP window specifies the range of sequence numbers that might be sent before an acknowledgement is required

the **checksum** is calculated across the entire segment and is compared with the checksum in the header to make sure that there was no data lost or corrupted along the way.

finally, we have some **padding** which is just a sequence of zeros to ensure that the data payload section begins at the expected location.

***Control flags :-***

TCP flags are used within TCP packet transfers to indicate a particular connection state or provide additional information. Therefore, they can be used for troubleshooting purposes or to control how a particular connection is handled.There are a few TCP flags that are much more commonly used than others as such “SYN”, “ACK”, and “FIN”. However, in this post, we’re going to go through the full list of TCP flags and outline what each one is used for.

![](https://miro.medium.com/max/1400/1*kkjKOhVS3l7A2QmU3sqSzQ.jpeg)

* **SYN** — The SYN, or Synchronisation flag, is used as a first step in establishing a 3-way handshake between two hosts. Only the first packet from both the sender and receiver should have this flag set.
* **ACK** — The ACK flag, which stands for “Acknowledgment”, is used to acknowledge the successful receipt of a packet. As we can see from the diagram above, the receiver sends an ACK as well as a SYN in the second step of the 3-way handshake process to tell the sender that it received its initial packet.
* **FIN** — The FIN flag, which stands for “Finished”, means there is no more data from the sender. Therefore, it is used in the last packet sent from the sender.
* **URG** — The URG flag is used to notify the receiver to process the urgent packets before processing all other packets. The receiver will be notified when all known urgent data has been received.
* **PSH** — The PSH flag, which stands for “Push”, is somewhat similar to the URG flag and tells the receiver to process these packets as they are received instead of buffering them.
* **RST** — The RST flag, which stands for “Reset”, gets sent from the receiver to the sender when a packet is sent to a particular host that was not expecting it.

Handshake is a way for two devices to ensure that they’re speaking the same protocol and will be able to understand each other. Once the three way handshake is complete, the TCP connection is established

***Three way handshake(to start )***

**A three**-**way handshake** is a method used in a TCP/IP network to create a connection between a local host/client and server. It is **a three**-step method that requires both the client and server to exchange SYN and ACK (acknowledgment) packets before actual data communication begins.

![](https://miro.medium.com/max/1400/1*GhTVZgKw9_FAAwCJsE3hsQ.jpeg)

***four way handshake — (to stop)***

it takes **four segments** to terminate a connection since a **FIN** and an **ACK** are required in each direction.

(1) send **FIN flag**\
(2) received **FIN** is acknowledged (**ACK**) by TCP\
(3) elater the application that received the end-of-file will close its socket. This causes its TCP to send a **FIN**.\
(4) TCP on the system that receives this final **FIN** acknowledges (**ACK**) the **FIN**.

![](https://miro.medium.com/max/1400/1*WrntHiXU_DHPMdueYA7qgw.jpeg)

Sockets — A socket is the instantiation of an endpoint in a potential TCP connection. An instantiation is the actual implementation of something defined elsewhere. TCP sockets require actual programs to instantiate them. You can contrast this with a port which is more of a virtual descriptive thing. In other words, you can send traffic to any port you want, but you’re only going to get a response if a program has opened a socket on that port. TCP sockets can exist in lots of states. And being able to understand what those mean will help you troubleshoot network

*TCP connection status*

**different sockets and their use in tcp connection —** [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.halu101/constatus.htm)

![](https://miro.medium.com/max/1400/1*sC1QLAtgl_XZUUKPpob6qQ.jpeg)

*TCP connection status*

**different sockets and their use in tcp connection —** [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.halu101/constatus.htm)

**‘’UDP”**

*REMEMBER “just send and pray…….”*

UDP doesn’t rely on connections and it doesn’t even support the concept of an acknowledgement. With UDP, you just set a destination port and send the packet. This is useful for messages that aren’t super important. *A great example of UDP is streaming video*. Let’s imagine that each UDP datagram is a single frame of a video. For the best viewing experience, you might hope that every single frame makes it to the viewer but it doesn’t really matter if a few get lost along the way. A video will still be pretty watchable unless it’s missing a lot of its frames. By getting rid of all the overhead of TCP, you might actually be able to send higher quality video with UDP. That’s because you’ll be saving more of the available bandwidth for actual data transfer instead of the overhead of establishing connections and acknowledging delivered data segments.

***FIREWALL***

![](https://miro.medium.com/max/1400/1*M_3R5UNWqfE_qC9FznkCqA.jpeg)

A firewall is just a device that blocks traffic that meets certain criteria. Firewalls are a critical concept to keeping a network secure since they are the primary way you can stop traffic you don’t want from entering a network.

Firewalls that operate at the transportation layer will generally have a configuration that enables them to block traffic to certain ports while allowing traffic to other ports. Let’s imagine a simple small business network. The small business might have one server which hosts multiple network services. This server might have a web server that hosts the company’s website, while also serving as the file server for a confidential internal document.

A firewall placed at the perimeter of the network could be configured to allow anyone to send traffic to port 80 in order to view the web page. At the same time, it could block all access for external IPs to any other port. So that no one outside of the local area network could access the file server.

**reference : —**

**1.** <https://www.coursera.org/learn/computer-networking/home/welcome>

2 . <https://www.amazon.com/Computer-Networking-Top-Down-Approach-Edition/dp/0132856204>

[](https://medium.com/tag/internet?source=post_page-----d05399d77782---------------internet-----------------)