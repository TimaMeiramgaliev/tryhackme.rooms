# [Wireshark: The Basics](https://tryhackme.com/room/wiresharkthebasics) [Easy]
### Learn the basics of Wireshark and how to analyse protocols and PCAPs.


## [TASK 1] Introduction
Wireshark is an open-source, cross-platform network packet analyser tool capable of sniffing and investigating live traffic and inspecting packet captures (PCAP). It is commonly used as one of the best packet analysis tools. In this room, we will look at the basics of Wireshark and use it to perform fundamental packet analysis.

### Which file is used to simulate the screenshots?
#### Answer: http1.pcapng

### Which file is used to answer the questions?
#### Answer: Exercise.pcapng


## [TASK 2] Tool Overview 
Why wireshark?
Network administrators use it to troubleshoot network problems
Network security engineers use it to examine security problems
QA engineers use it to verify network applications
Developers use it to debug protocol implementations
People use it to learn network protocol internals 

#### Read the "capture file comments". What is the flag?
Statistics->Capture File Properties


![Screenshot_20220808_064946](https://user-images.githubusercontent.com/86546994/183318598-7cb1fb82-ad7f-439c-ad93-1d994aa0e15e.png)


#### Answer: TryHackMe_Wireshark_Demo 

#### What is the total number of packets?
To find all packets you can scroll down till the end and find last packet or just open Statistics->Capture File Properties
![Screenshot_20220808_062328](https://user-images.githubusercontent.com/86546994/183318015-079f9a9b-d752-43c1-b176-45714a6a9f4d.png) 

#### Answer: 58620

#### What is the SHA256 hash value of the capture file?
Again open Statistics->Capture File Properties 


![Screenshot_20220808_064722](https://user-images.githubusercontent.com/86546994/183318455-2e1cd62e-8f3a-473d-babc-cb7d40e482dc.png)
#### Answer: f446de335565fb0b0ee5e5a3266703c778b2f3dfad7efeaeccb2da5641a6d6eb

## [TASK 3] Packet Dissection 
#### Packet Dissection 
Packet dissection is also known as protocol dissection, which investigates packet details by decoding available protocols and fields

#### Packet Details
You can click on a packet in the packet list pane to open its details (double-click will open details in a new window). Packets consist of 5 to 7 layers based on the OSI model. We will go over all of them in an HTTP packet from a sample capture. The picture below shows viewing packet number 27.

#### View packet number 38. Which markup language is used under the HTTP protocol? 
So, open the packet witrh number 38 and see some details

![Screenshot_20220808_065736](https://user-images.githubusercontent.com/86546994/183319073-ea3787b6-91e7-4ecd-8868-87b7c691f4bf.png)


#### Answer: eXtensible Markup Language

#### What is the arrival date of the packet? (Answer format: Month/Day/Year)
In The Frame (Layer 1) you can find specific details related to Physical Layer of OSI model

![Screenshot_20220808_065955](https://user-images.githubusercontent.com/86546994/183319251-a6a753aa-96c0-4952-8610-6c7bd1e16e80.png)


#### Answer: 05/13/2004

#### What is TTL value?
Information related to time to live we can find in IP layer

![Screenshot_20220808_070415](https://user-images.githubusercontent.com/86546994/183319496-16dbf3b1-2e55-4939-b8bd-450443cb523c.png)


#### Answer: 47


#### What is the TCP payload size?
By looking at Reassembled TCP Segments we can find our 38 number packet with its payload size

![Screenshot_20220808_070731](https://user-images.githubusercontent.com/86546994/183319708-8455ffe9-6641-48c3-b604-0b37caf1e220.png)


#### Answer: 424

#### What is the e-tag value&
Open Hypertext Transfer Protocol->Http/1.1 200 OK\r\n->Expert Info, here you will find information about E-tag

#### Answer: 9a01a-4696-7e354b00

## [TASK 4] Packet Navigation 
#### Packet Numbers
Wireshark calculates the number of investigated packets and assigns a unique number for each packet. More about this - https://www.wireshark.org/docs/wsug_html_chunked/ChUsePacketListPaneSection.html

#### Go to Packet
You can easily jump to specific packets with one of the menu items in the Go menu using packet unique number.

#### Search the "r4w" string in packet details. What is the name of artist 1?

Press ctrl + f and type r4w, it will give the required information

![Screenshot_20220808_141044](https://user-images.githubusercontent.com/86546994/183371042-a638abb6-e739-4d80-8e5f-3cd19ff80bdb.png)


#### Answer: r4w8173

#### Go to packet 12 and read the comments. What is the answer?
Go to the Edit->Packet comment and read given comment.


![Screenshot_20220808_073523](https://user-images.githubusercontent.com/86546994/183321626-08604e2b-afb4-4e74-af76-212180399c1a.png)


As the comment we have the tip to go to packet 39765 and do some actions in order to find flag.
Easiest way is opening File->Export Objects->HTTP and directly download the JPEG image
After in terminal we can convert it to MD5 Hash using 'md5sum [file name]'


![Screenshot_20220808_133806](https://user-images.githubusercontent.com/86546994/183365035-bda21fba-792b-4369-a47d-b17dbf76267a.png)


#### Answer: 911cd574a42865a956ccde2d04495ebf


#### There is a ".txt" file inside the capture file. Find the file and read it; what is the alien's name?
Using the same method we can download txt file or whatever we need. The file name is 'Note.txt', if we open it, we will find exact solution.

#### Answer: PACKETMASTER


#### Look at the expert info section. What is the number of warnings?
To open Expert info go to Analyze->Expert Information. (Note: Disable group by summary option)


![Screenshot_20220808_134607](https://user-images.githubusercontent.com/86546994/183366504-cd3d2c20-dc12-4b96-8e2f-ae47a62bc6ae.png)


#### Answer: 1636

## [TASK 5] Packet Filtering 
#### Packet Filtering 
Wireshark has two filtering languages: capture filters and display filters. Capture filters are used for filtering when capturing packets and are discussed in Section 4.10, “Filtering while capturing”. Display filters are used for filtering which packets are displayed and are discussed below. For more information about display filter syntax, see the wireshark-filter(4) man page. https://www.wireshark.org/docs/man-pages/wireshark-filter.html
https://www.wireshark.org/docs/wsug_html_chunked/ChCapCaptureFilterSection.html

#### Go to packet number 4. Right-click on the "Hypertext Transfer Protocol" and apply it as a filter. 
You already know how to move through packets, open the packet number 4 and apply as a filter Hypertext Transfer Protocol

![Screenshot_20220808_135426](https://user-images.githubusercontent.com/86546994/183368176-9a6edfe5-deb9-44ee-932c-8897f91a322a.png)


#### Answer: http


#### What is the number of displayed packets?

Open Statistics->Capture File Properties

#### Answer: 1089

#### Go to packet number 33790 and follow the stream. What is the total number of artists?
Go to the packet 33790 right click on it and Follow HTTP Stream.
By analyzing packet you will understand that there is only 3 artist
#### Answer: 3


#### What is the name of the second artist?
Use as filter 'artist=2'


![Screenshot_20220808_140633](https://user-images.githubusercontent.com/86546994/183370254-0a15bf8a-3d02-4179-a5b0-62690b991f71.png)


#### Answer: Blad3

## [TASK 6] Conclusion 
#### Conclusion
Congratulations! You just finished the "Wireshark: The Basics" room. In this room, we covered Wireshark, what it is, how it operates, and how to use it to investigate traffic captures. 
