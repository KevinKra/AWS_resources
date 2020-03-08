# Advanced Networking Certification

## Networking Refresher

### 7 Layers of the OSI Model

> 7 Layer OSI model exists to ensure that machines can communicate despite stack differences.

> All People Seem To Need Data Processing

#### Networking Stack's 7 Logical Components
- 7. Application
- 6. Presentation
- 5. Session
- 4. Transport
- 3. Network
- 2. Datalink
- 1. Physical

When you generate data in one application (machine A), that data is injected at the application layer and it rigidly travels down (from 7 to 1) down the _Network Stack_ until it reaches machine B and travels up (from 1 to 7) the Network Stack of machine B and then is consumed by the application of machine B.

#### Physical Layer (1)
- Represents the electrical and physical representation of the system. Includes everything from the cable type, radio frequency link, as well as the layout of pins, voltages, and other physical requirements. 

#### Datalink Layer (2)
- Provides node-to-node data transfer (between two directly connected nodes), and also handles error correction from the physical layer. Two sublayers exist here - Media Access Control (MAC) and Link Control (LLC) layer.
- Machine A can, _assuming it knows the address_, communicate with Machine B. Each machine has a hardware address, aka **MAC Address**. If A knows B's MAC Address it can communicate it. 
- Controls sequencing and flow control. Machine B can communicate to Machine A if it's sending data too fast and Machine A can slow down.
- Handles **Error Correction**. If Data is damaged by the Physical layer it will know and it can resend it.
- Handles **Sequencing**. If a **frame** is received out of order machine B knows how to reorder the frames.

#### Network Layer (3)
Machines are no longer communicating with frames, instead they are using packets. 
- Packets don't use hardware addresses, they use IP addresses.
- Packet contains a source and destination address. The device receiving the packet might not be the destination, could be the router.
- **No Error Checking. Purely IP.**
- Protocols that use this layer: **IP, IPX, ICMP**

#### Transport Layer (4)
- No longer uses Packets, instead uses Segments or Data Segments.
- Host-to-Host flow control and some error correction is added as well.
- Protocols that use this layer: **TCP/UDP**
- No form of ongoing connection. This layer, and the ones below it in the Network Stack (above here), just allow for the sending of packets and segments from A to B or vice versa.
- **Encapsulation/De-Encapuslation**

#### Session Layer (5)
- Start of on-going sessions. Allows open connection between machines.
- Handles the perception of a session.
- Adds the concept of ports. Allows multiple services to run and be addressed on one host.

#### Presentation Layer (6)
- The preparation and translation of application format to network format or network format to application format. This layer "presents" data fro the application or the network.
- A good example of this is encryption and decryption of data for secure transmission - this happens on layer 6.

#### Application Layer (7)
- What the end user interacts with. Chrome, FireFox, Slack, etc.


---

## Design and Implement AWS Networks

## Design and Implement Hybrid Networks

## Configure Network Integration With Application Services

## Manage Optimise And Troubleshoot the Network
