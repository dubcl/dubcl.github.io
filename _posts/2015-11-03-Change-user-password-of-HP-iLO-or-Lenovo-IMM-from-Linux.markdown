---
published: true
---



## Change user password of HP iLO or Lenovo IMM from Linux

When you have a new machine and you forgot write the Administrator password on any paper or note before installing, you can change this from you linux install with ipmitools.

First, if you read the pass post about [Assign an IP to HP iLO or IBM System X from Linux](http://albornoz.rocks/assign-an-ip-to-hp-ilo-from-linux/), you know how get the configuration channel, if not, read it ;)

Once you get the channel you need to list iLO / IMM users, for example:

```code-bash
ipmitool user list 2
```

You see something like this:

```code-bash
ipmitool user list 2
ID  Name	     Callin  Link Auth	IPMI Msg   Channel Priv Limit
1   Administrator    true    false      true       ADMINISTRATOR
2   (Empty User)     true    false      false      NO ACCESS
3   (Empty User)     true    false      false      NO ACCESS
4   (Empty User)     true    false      false      NO ACCESS
5   (Empty User)     true    false      false      NO ACCESS
6   (Empty User)     true    false      false      NO ACCESS
7   (Empty User)     true    false      false      NO ACCESS
8   (Empty User)     true    false      false      NO ACCESS
9   (Empty User)     true    false      false      NO ACCESS
10  (Empty User)     true    false      false      NO ACCESS
11  (Empty User)     true    false      false      NO ACCESS
12  (Empty User)     true    false      false      NO ACCESS
```

Now we know the Administrator ID, then now we can change their password with:

```code-bash
ipmitool user set password 1
```

And put the password, for example:

```code-bash
ipmitool user set password 1
Password for user 1: 
Password for user 1: 
```

Now if you go to web login, use the user and you new password.
