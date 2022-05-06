# [Game Zone](https://tryhackme.com/room/gamezone) [Easy]
### Learn to hack into this machine. Understand how to use SQLMap, crack some passwords, reveal services using a reverse SSH tunnel and escalate your privileges to root!

## [TASK 1] Deploy the vulnerable machine 
This room will cover SQLi (exploiting this vulnerability manually and via SQLMap), cracking a users hashed password, using SSH tunnels to reveal a hidden service and using a metasploit payload to gain root privileges. 

#### Deploy the machine and access its web server.

#### Answer: No answer needed

#### What is the name of the large cartoon avatar holding a sniper on the forum?

Go to given IP address and see page with charachter.


![Screenshot_20220506_122113](https://user-images.githubusercontent.com/86546994/167077912-bbcec367-e61f-46b9-b5ad-e52182d21708.png)


It is clear that character from the "Hitman" franchise. I dont know the name of character, so let's find his name in any website.


![Screenshot_20220506_122243](https://user-images.githubusercontent.com/86546994/167078113-7da347bd-8ee9-4185-8504-ebb521dd8508.png)


#### Answer: Agent 47


## [TASK 2] Obtain access via SQLi 
In this task you will understand more about SQL (structured query language) and how you can potentially manipulate queries to communicate with the database.

The query which web site uses looks like `SELECT * FROM users WHERE username = admin AND password := ' or 1=1 -- -`, we can use it in order to try to gain admin access.

#### Use ' or 1=1 -- - as your username and leave the password blank.
#### When you've logged in, what page do you get redirected to?

#### Answer: Portal.php

## [Task 3] Using SQLMap
Sqlmap is an open source penetration testing tool that automates the process of detecting and exploiting SQL injection flaws and taking over of database servers. It comes with a powerful detection engine, many niche features for the ultimate penetration tester and a broad range of switches lasting from database fingerprinting, over data fetching from the database, to accessing the underlying file system and executing commands on the operating system via out-of-band connections.


#### In the users table, what is the hashed password?

We need to intercept request using burp suite, configure foxy proxy and get request.


![Screenshot_20220506_160352](https://user-images.githubusercontent.com/86546994/167111539-24a8a282-4763-4b2e-91e5-49622f16a628.png)


After save the request to file.


![Screenshot_20220506_160827](https://user-images.githubusercontent.com/86546994/167112032-543ca018-c375-4ae5-ac85-3929edbdb828.png)


Now, we a ready to run this command:
`sqlmap -r [path to your request] --dbms=mysql --dump`

There will be some options while running sqlmap, to get result us me you should answer:
So, we got result.


![Screenshot_20220506_162549](https://user-images.githubusercontent.com/86546994/167114798-58066d67-445d-4813-bbdd-a4d52be664fc.png)


#### Answer: ab5db915fc9cea6c78df88106c6500c57f2b52901ca6c0c6218f04122c3efd14


#### What was the username associated with the hashed password?

#### Answer: agent47

#### What was the other table name?

#### Answer: post

## [TASK 4] Cracking a password with JohnTheRipper
John the Ripper (JTR) is a fast, free and open-source password cracker.

#### What is the de-hashed password?

First, we need to save the hash in some file, lets call it hash.txt
Them we need to identify hash type, you can use online tools or hash id tool https://github.com/blackploit/hash-identifier
After we can run our command

`john --wordlist=[path to wordlist] --format=[hash type] [path to hash]`

Identify hash:


![Screenshot_20220506_163740](https://user-images.githubusercontent.com/86546994/167116440-fd20e14a-5db0-415f-9589-a02f144beec2.png)


Hash type is most likely SHA-256. Now, we got everything to run command
`john --wordlist=/usr/share/wordlists/rockyou.txt --format=Raw-SHA256 hash.txt`


![Screenshot_20220506_164022](https://user-images.githubusercontent.com/86546994/167116737-1f3c8ba0-2600-4ed7-82db-bad46ea46844.png)


#### Answer: videogamer124


#### Now you have a password and username. Try SSH'ing onto the machine.
#### What is the user flag?

In order to connect ssh we need to run command
ssh [username]@[IP]
And after type the password


![Screenshot_20220506_164404](https://user-images.githubusercontent.com/86546994/167117199-131322ba-deec-4ad3-baf9-f1e6dff6d9cf.png)


#### Answer: 649ac17b1480ac13ef1e4fa579dac95c


## [TASK 5] Exposing services with reverse SSH tunnels 

run `ss -tulpn` in ssh connected machine

#### How many TCP sockets are running?

#### Answer: 5
