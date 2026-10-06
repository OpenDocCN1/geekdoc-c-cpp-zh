
would have to cast each individual element to a string when we print it. We can overcome this limitation with map, which takes every element in an array and runs a function against it:
"".join(map(str,mask))

By using map, we convert each integer in our netmask to a string. This leaves us with a list of strings. Next we use join to join them together. The join function works by using a delimiter to assemble the elements of a list into a string where each element is separated by that delimiter. We should have all we need to combine our final program. Let's try out, and verify that everything is working:

```python
#!/usr/bin/python
import sys
# Get address string and cidr string from command line
(addrString,cidrString) = sys.argv[1].split('/')
# split address into octets and turn cidr into int
addr = addrString.split('.')
cid = int(cidrString)
#initialize the netmask and calculate based on cidr mask
mask = [0,0,0,0]
for i in range(cidr):
mask[i/8] = mask[i/8] + (1 << (7 - i % 8))
#initialize net and binary and netmask with addr to get
net = []
for i in range(4):
net.append(int(addr[i]) & mask[i])
#duplicate net into broad array, gather host bits, and
generate #broadcast
broad = list(net)
brange = 32 - cidr
for i in range(brange):
broad[3 - i/8] = broad[3 - i/8] + (1 << (i % 8))
# Print information, mapping integer lists to
# easy printing
print "Address: " , addrString
print "Netmask: " , "".join(map(str,mask))
print "Network: " , "".join(map(str,net))
print "Broadcast: " , "".join(map(str,broad))
```

Now, examine the output in Fig. 2.6.

# root@mostdefinitelynotkali: ~/Desktop

```
root@mostdefinitelynotkali:~/Desktop/.subnet.py 192.168.1.1/24
Address: 192.168.1.1
Netmask: 255.255.255.0
Network: 192.168.1.0
Broadcast: 192.168.1.255
Address: 192.168.1.1
Netmask: 255.255.255.0
Network: 192.168.1.0
Broadcast: 192.168.1.255
Address: 192.168.1.1
Netmask: 255.255.255.0
Network: 192.168.1.0
Broadcast: 192.168.1.255
Address: 192.168.1.1
Netmask: 255.255.255.0
Network: 192.168.1.0
Broadcast: 192.168.1.255
Address: 192.168.1.1
Netmask: 255.255.255.0
Network: 192.168.1.0
Broadcast: 192.168.1.255
```

# FIGURE 2.6 Fun with subnets.

We now have a working code example that uses lists in a number of ways. While this provides some basics for using lists, we will explore some of these topics further in examples in the next section of this chapter.

## Dictionaries
use dictionaries when we have list elements that we'd like to label. For example, we could be mapping IDs to employee names, or associating multiple vulnerabilities to a specific host.

To examine dictionaries, let's start with a practical example. A company may have a standard initial password for users based on some pattern. This could include using letters and numbers that have some relevance to the individual—e.g., first character of first name plus employee ID assigned by Human Resources. If we find a shadowed password file, we may be able to determine which users have a default password if we know how the passwords are computed.

Say we have found a password file:
kevin:j5PRTBmoSymUI:42:42:Kevin,,, 42:/home/kevin:/bin/bash
ryan:A1QD3nPMW5e:1000:1000:Ryan,,, 431/home/ryan:/bin/bash
jason:aPg1C.EYR0db:1001:1001:Jason,,, 739/home/jason:/bin/bash
don:JCZWI:1002:1002:Don,,, 831/home/don:/bin/bash
ed:yN:1337:1337:Ed,,, 337/home/ed:/bin/bash

# Note
A quick refresher about the field: the first field is the username, the second field is the GECO information, the third field is the UID, the fourth field is the home, the fifth field is the shell.

Using dictionaries to crack passwords, we can use the `crypt` module to hash potential passwords and compare them with the hashes in the file. For example, we use a dictionary to store the results.

```python
#!/usr/bin/python
import sys
import crypt
f = open(sys.argv[1],"r+")
lines = f.readlines()
f.close()

found = []
for line in lines:
    data = line.split(':')
    # Set username and password to first 2 fields
    user,password = data[0:2]
    geco = data[4].split(',')
    # Create password guess using first char of name and last field
    guess = geco[0][0] + geco[-1]
    # Assign salt as first 2 characters of crypted password
    salt = password[0:2]
    # Check crypted value to see if matches, if yes put in found
    if crypt.crypt(guess,salt) == password:
        userInfo = { "user": user, "pass": guess, "home" : data[5],
                    "uid" : data[2] , "name" : geco[0] }
        found.append(userInfo)

for user in found:
    print "User : %s " % user['user']
    for k in user.keys():
        if k == "user":
            continue
        print "\t%s %s" (k,user[k])
```
