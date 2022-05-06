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
sqlmap is an open source penetration testing tool that automates the process of detecting and exploiting SQL injection flaws and taking over of database servers. It comes with a powerful detection engine, many niche features for the ultimate penetration tester and a broad range of switches lasting from database fingerprinting, over data fetching from the database, to accessing the underlying file system and executing commands on the operating system via out-of-band connections.

#### In the users table, what is the hashed password?



#### Answer: 
