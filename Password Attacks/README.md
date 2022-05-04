# [Password Attacks](https://tryhackme.com/room/passwordattacks) [Hard]
### This room introduces the fundamental techniques to perform a successful password attack against various services and scenarios.


## [TASK 1] Introduction 
This room is an introduction to the types and techniques used in password attacks. We will discuss the ways to get and generate custom password lists. The following are some of the topics we will discuss:
1.    Password profiling
2.    Password attacks techniques
3.    Online password attacks


## [TASK 2] Password Attacking Techniques 
In this room, we will discuss the techniques that could be used to perform password attacks. 
Password Cracking vs. Password Guessing

This section discusses password cracking terminology from a cybersecurity perspective. Also, we will discuss significant differences between password cracking and password guessing. Finally, we'll demonstrate various tools used for password cracking, including Hashcat and John the Ripper.

#### Which type of password attack is performed locally?
#### Answer: Password cracking


## [TASK 3] Password Profiling #1 - Default, Weak, Leaked, Combined , and Username Wordlists
#### Default passwords
Sometimes it's good practice to use the default password to break into a service. A default password is a standard pre-configured password for a device. Such passwords are the default configuration for many devices and, if unchanged, present a serious security risk. Famous rockyou.txt comes from data breach occured in December 2009, when the company "RockYou" experienced a data breach resulting in the exposure of over 32 million user accounts. Examples: admin, 123, root. Very often the default password is found in routers and virtual machines. Website that provide default passwords: https://cirt.net/passwords

#### Weak Passwords
A weak password is short, common, a system default, or something that could be rapidly guessed by executing a brute force attack using a subset of all possible passwords, such as words in the dictionary, proper names, words based on the user name or common variations on these themes.

#### Leaked Passwords
Leaked password database is an aggregated collection of login credentials known to have been exposed. As new breaches and leaks occur, security researchers work to discover data breaches to add and process compromised credentials. There are many different sites where you can check for leaked passwords. https://www.avast.com/hackcheck#pc

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

#### Answer:

#### Perform a brute-force attack against the following MD5 hash: e48e13207341b6bffb7fb1622282247b. What is the cracked value? Note the password is a 4 digit number: [0-9][0-9][0-9][0-9]

#### Answer:
