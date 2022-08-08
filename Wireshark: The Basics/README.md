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


#### Answer: 

#### Go to packet 12 and read the comments. What is the answer?
Go to the Edit->Packet comment and read given comment.


![Screenshot_20220808_073523](https://user-images.githubusercontent.com/86546994/183321626-08604e2b-afb4-4e74-af76-212180399c1a.png)


As the comment we have the tip to go to packet 39765 and do some actions in order to find flag.

In order to specify `@` charachter in a list, we should follow this options:
`    , for all uppercase letters
    @ for all lowercase letters
    % for all numeric characters
    ^ for all special characters`
`5 5` -> represents the length of generated words
`-t` option -> to use specific pattern

![Screenshot_20220504_183221](https://user-images.githubusercontent.com/86546994/166684097-d4691e3e-cc1a-41cf-8836-41b9bd6cd90d.png)

#### Answer: crunch 5 5 -t "THM^! " -o tryhackme.txt

## [TASK 5] Offline Attacks - Dictionary and Brute-Force
#### Dictionary attack
A dictionary attack is a method of guessing password by systematically entering every word in a dictionary as a password. 

#### Brute-Force attack
A brute force attack uses trial-and-error to guess login info, encryption keys, or find a hidden web page. This method is used to guess the victim's password by sending standard password combinations.

Usefull tools: hashcat, john the ripper

#### Considering the following hash: 8d6e34f987851aa599257d3831a1af040886842f. What is the hash type?
To identify hash type we can use different tools, I prefer to use `hash id`. You can download it from github - https://github.com/blackploit/hash-identifier.
Type `python3 hash-id.py` and paste hash

![Screenshot_20220504_185846](https://user-images.githubusercontent.com/86546994/166686381-cb0bfa3c-29e2-4c55-a56e-53fd58e19087.png)

#### Answer: SHA-1

#### Perform a dictionary attack against the following hash: 8d6e34f987851aa599257d3831a1af040886842f. What is the cracked value? Use rockyou.txt wordlist.

To perform dictionary attack firstly we need to identify hash type. We already know, that hash type is `SHA-1`.
Let's use `John the ripper`, here the simple usage

john --wordlist=[path to wordlist file] --format=[hash format] [path to hash]
Can save our hash in hash1.txt
echo '8d6e34f987851aa599257d3831a1af040886842f' > hash1.txt
Now, we have txt file with hash and we know hash format, we can run `john the ripper`

`john --wordlist=/usr/share/wordlists/rockyou.txt --format=Raw-MD5 hash1.txt`

![Screenshot_20220505_182055](https://user-images.githubusercontent.com/86546994/166921724-54a7d397-99db-4a2e-9f25-5e4940c6f649.png)

P.s if you crack this hash first time, result will appear in terminal. After cracking same hash will show no result. To see, type john --show=[hash format] [path to hash]

#### Answer: sunshine

#### Perform a brute-force attack against the following MD5 hash: e48e13207341b6bffb7fb1622282247b. What is the cracked value? Note the password is a 4 digit number: [0-9][0-9][0-9][0-9]

Let's john the ripper again. You know steps, just reminder!

1. Save hash to txt file

2. Identify hash type

3. Run the command `john --wordlist=[path to wordlist file] --format=[hash format] [path to hash]`

![Screenshot_20220505_182734](https://user-images.githubusercontent.com/86546994/166922763-aa8b976a-93fa-4ebe-b562-c7f9fa32d429.png)

#### Answer: 1337

## [TASK 6] Offline Attacks - Rule-Based
#### Rule-Based
A rule-based password attack is a way of focusing a password cracking technique when an attacker knows which rules passwords in a particular system are based on, such as alphanumeric and eight characters long.
For this attack, we can use either hashcat or John the ripper.

`Az represents a single word from the original wordlist/dictionary using -p.

"[0-9]" append a single digit (from 0 to 9) to the end of the word. For two digits, we can add "[0-9][0-9]"  and so on.  

^[!@#$] add a special character at the beginning of each word. ^ means the beginning of the line/word. Note, changing ^ to $ will append the special characters to the end of the line/word.`

#### What would the syntax you would use to create a rule to produce the following: "S[Word]NN  where N is Number and S is a symbol of !@? 

#### Answer:  Az"[0-9][0-9]" ^[!@]

#### [TASK 7] Deploy the VM
`cewl -m 8 -w clinic.lst https://clinic.thmredteam.com/` run to create custom wordlit

#### [TASK 8] Online password attacks 
Online password attacks include procesess of guessing password of networked services like SSH, SNMP, FTP, POP3 and etc.

For this tasks we will use famous `Hydra` tool.

#### FTP
`hydra -L [path to username.txt] -P [path to password.txt] ftp://[IP]`

#### SMTP
`hydra -L [path to username.txt] -P [path to password.txt] smtp://[IP]`

#### SSH
`hydra -L [path to username.txt] -P [path to password.txt] ssh://[IP] -v`


#### Can you guess the FTP credentials without brute-forcing? What is the flag?
Go to website with default password lists - https://datarecovery.com/rd/default-passwords/
Here we need to find username and password related to ftp.
There are different default password, try all of them!

![Screenshot_20220505_195359](https://user-images.githubusercontent.com/86546994/166938685-82849f8a-9bfe-4dd7-9ae7-bbc8b4b701d8.png)

username: ftp and password: ftp looks suitable.

![Screenshot_20220505_195545](https://user-images.githubusercontent.com/86546994/166938885-8ead3aaf-232f-4758-ae79-f01d5d3e9c85.png)

After connection, go to `Files` directory and type `get flag.txt` to copy file to your local machine.

#### Answer THM{d0abe799f25738ad739c20301aed357b}


#### In this question, you need to generate a rule-based dictionary from the wordlist clinic.lst in the previous task. email: pittman@clinic.thmredteam.com against 10.10.200.112:25 (SMTP).
#### What is the password? Note that the password format is as follows: [symbol][dictionary word][0-9][0-9].

We know how to create rules-based dictionary using `john the ripper`.

In /etc/john/john.conf we should write our created rule


![Screenshot_20220512_181354](https://user-images.githubusercontent.com/86546994/168072289-5d3fb40e-f8aa-4777-8b4d-be3a59b37aa5.png)

Now, we can create a wordlist using our wordlist 

`john --wordlist=clinic.lst --rules=[Rule name] --stdout > [File where you want to save]`

run the bruteforce attack using generated password

`hydra -l pittman@clinic.thmredteam.com -P [generated list] smtp://[IP]:25`

#### ANSWER: !multidisciplinary00

#### Perform a brute-forcing attack against the phillips account for the login page at http://10.10.187.109/login-get using hydra? What is the flag?

as a password list, we gonna use clinic.lst
Here you can more about brute forcing login pages - https://russianblogs.com/article/1635894923/
`hydra -l phillips -P clinic.lst 10.10.6.182 http-get-form "/login-get/index.php:username=phillips&password=^PASS^:S=logout.php" -f`

#### ANSWER: Paracetamol

#### Perform a rule-based password attack to gain access to the burgess account. Find the flag at the following website: http://10.10.6.182/login-post/. What is the flag?

#### Note: use the clinic.lst dictionary in generating and expanding the wordlist!

we should crate new list using default john the ripper rule - Single-Extra
`john --wordlist=clinic.lst --rules=Single-Extra --stdout > [File where you want to save]`
And run the command
`hydra -l burgess -P generated list [IP] http-post-form "/login-post/index.php:username=burgess&password=^PASS^:S=logout.php" -f`

#### Answer: OxytocinnicotyxO
