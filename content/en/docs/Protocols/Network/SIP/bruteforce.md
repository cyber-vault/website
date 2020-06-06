---
title: "Brute Force"
linkTitle: "Brute Force"
date: 2020-05-31T16:20:47+02:00
draft: false
description: "A brute force attack can be performed on FTP servers." 
---
Brute forcing Passwords and usernames from FTP servers is possible but usually as a last resort. The other methods of attack are a lot beter. 

Brute forcing is random guessing or educated guessing. 

The attack consists of trying the passwrod and username and then trying to perform actions that require special permissions like for example uploads or creation of files or folders.

## Low-Level
The password and username are send to the server. If the return is 2XX then the password and username are correct.

If the error that is returned is 5XX then the password is incorrect.
The exact string that is send is :

```
USER <username> 
PASS <password>
```

##  Perform
This attack can be performed using a tool named Hydra. It is also relatively trivial to write a tool to perform a brute force attack.


##  Mitigation
It is possible to mitigate the attack by monitoring and alerting on it. The key metric to look for is if a user is retrying passwords over and over again. If the same IP tries a lot of logins with or without 
