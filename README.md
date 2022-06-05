# Lab 4
![image](https://user-images.githubusercontent.com/25465133/172073613-7f80740d-ad61-4deb-bc68-e331b150cb5c.png)
1. What is the 48-bit Ethernet address of your computer?
```
00:d0:59:a9:3d:68
```

2. What is the 48-bit destination address in the Ethernet frame? Is this the Ethernet  address of gaia.cs.umass.edu? (Hint: the answer is no). What device has this as its Ethernet address? [Note: this is an important question, and one that students sometimes get wrong. Re-read pages 468-469 in the text and make sure you understand the answer here.]
```
00:06:25:da:af:73 This is the ethernet address of the router the computer is
connected to.
```

3. Give the hexadecimal value for the two-byte Frame type field. What upper layer protocol does this correspond to?
```
0x0800 - IPv4
```

4. How many bytes from the very start of the Ethernet frame does the ASCII “G” in “GET” appear in the Ethernet frame?
```
byte 54, aka the 55th byte
```

![image](https://user-images.githubusercontent.com/25465133/172073649-d23f3b8c-0a7e-40dd-812b-744350d3b451.png)
5. What is the value of the Ethernet source address? Is this the address of your computer, or of gaia.cs.umass.edu (Hint: the answer is no). What device has this as its Ethernet address?
```
00:06:25:da:af:73 This is the ethernet address of the router the computer is
connected to.
```

6. What is the destination address in the Ethernet frame? Is this the Ethernet address of your computer?
```
00:d0:59:a9:3d:68 Yes
```

7. Give the hexadecimal value for the two-byte Frame type field. What upper layer protocol does this correspond to?
```
0x0800 - IPv4
```

8. How many bytes from the very start of the Ethernet frame does the ASCII “O” in “OK” (i.e., the HTTP response code) appear in the Ethernet frame?
```
byte 67, aka the 68th byte
```

9. Write down the contents of your computer’s ARP cache. What is the meaning of each column value?
![image](https://user-images.githubusercontent.com/25465133/172073681-87359aa0-7346-415d-a76a-84af5c7f38d3.png)
```
The table shows the ip addresses, Mac addresses, and network interfaces
associated with each entry.
```

![image](https://user-images.githubusercontent.com/25465133/172073692-dab51931-cd6e-44a1-ac00-6275fbfb6611.png)
10. What are the hexadecimal values for the source and destination addresses in the Ethernet frame containing the ARP request message?
```
Source: 00:d0:59:a9:3d:68
Destination ff:ff:ff:ff:ff:ff
```

11. Give the hexadecimal value for the two-byte Ethernet Frame type field. What upper layer protocol does this correspond to?
```
0x0806 - ARP
```

12. Download the ARP specification from ftp://ftp.rfc-editor.org/in-notes/std/std37.txt. A readable, detailed discussion of ARP is also at http://www.erg.abdn.ac.uk/users/gorry/course/inet-pages/arp.html.
  - How many bytes from the very beginning of the Ethernet frame does the  ARP opcode field begin?
```
byte 20, the 21st byte
```

  - What is the value of the opcode field within the ARP-payload part of the  Ethernet frame in which an ARP request is made?
```
0001
```

  - Does the ARP message contain the IP address of the sender?
```
Yes (192.168.1.105)
```

  - Where in the ARP request does the “question” appear – the Ethernet address of the machine whose corresponding IP address is being queried?
```
The end, the Target IP Address (192.168.1.1)
```

![image](https://user-images.githubusercontent.com/25465133/172073749-fcd531aa-9202-46eb-ba02-3792844ea853.png)
13. Now find the ARP reply that was sent in response to the ARP request.
  - How many bytes from the very beginning of the Ethernet frame does the  ARP opcode field begin?
```
byte 20, the 21st byte
```

  - What is the value of the opcode field within the ARP-payload part of the  Ethernet frame in which an ARP response is made?
```
0002
```

  - Where in the ARP message does the “answer” to the earlier ARP request  appear – the IP address of the machine having the Ethernet address whose corresponding IP address is being queried?
```
Sender MAC address (00:06:25:da:af:73)
```

13. What are the hexadecimal values for the source and destination addresses in the Ethernet frame containing the ARP reply message?
```
Source: 00:06:25:da:af:73
Destination: 00:d0:59:a9:3d:68
```

15. Open the ethernet-ethereal-trace-1 trace file in http://gaia.cs.umass.edu/wireshark-labs/wireshark-traces.zip. The first and second ARP packets in this trace correspond to an ARP request sent by the computer running Wireshark, and the ARP reply sent to the computer running Wireshark by the computer with the ARP-requested Ethernet address. But there is yet another computer on this network, as indicated by packet 6 – another ARP request. Why is there no ARP reply (sent in response to the ARP request in packet 6) in the packet trace?
```
This computer is neither the router or the computer sending the ARP request. The
answer is only sent to the computer making the request so only the router and
sender would see the reply.
```

## Extra Credit:
1. The arp command: arp -s InetAddr EtherAddr allows you to manually add an entry to the ARP cache that resolves the IP address InetAddr to the physical address EtherAddr. What would happen if, when you manually added an entry, you entered the correct IP address, but the wrong Ethernet address for that remote interface?
```
Though incorrect, the command would still make a static entry into the ARP table
until the computer reboots.

If a packet was sent from this computer to the ip address, depending on the
configuration of the network, a switch/router could either drop the packet, or
the router would get the correct MAC address for the IP address and replace the
invalid one in the header with the correct one.
```

2. What is the default amount of time that an entry remains in your ARP cache before being removed. You can determine this empirically (by monitoring the cache contents) or by looking this up in your operation system documentation. Indicate how/where you determined this value.
```
On macOS the default ARP cache time for a dynamic address is 20 minutes.

Found in arp info on my macOS device:
“The ARP cache is stored in the system routing table as dynamically-created host
routes.  The route to a directly-attached Ethernet network is installed as a
``cloning'' route (one with the RTF_CLONING flag set), causing routes to
individual hosts on that network to be created on demand.  These routes time out
periodically (normally 20 minutes after validated; entries are not validated
when not in use).”
```
