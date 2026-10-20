manages (administers) your Linux system and is commonly known as the superuser or system administrator. The login name for the superuser is root and the user ID is 0.

You can see the list of all user groups on your system by displaying the /etc/group file, shown as follows.

```
$ more /etc/group
root:x:0:
daemon:x:1:
bin:x:2:root,bin,daemon
sys:x:3:
adm:x:4:syslog,bob,ali,goldsmith,ravi
tty:x:5:
disk:x:6:
lp:x:7:
mail:x:8:
news:x:9:
uucp:x:10:
man:x:12:
proxy:x:13:
kmem:x:15:
dialout:x:20:davis,bob
fax:x:21:
voice:x:22:
cdrom:x:24:bob
floppy:x:25:
tape:x:26:
sudo:x:27:bob
audio:x:29:pulse
dip:x:30:bob
...
sambashare:x:130:bob,ali,ravi
lab:x:1001:davis,sam
faculty:x:1002:bob,sarwar,goldsmith,ravi,
ravi:x:1003:
goldsmith:x:1004:
bob:x:1005:
sarwar:x:1006:
$
```

There is one line in this file for every group on the system, each line having four colon-separated fields. The first field specifies the group name, the second specifies some information about the group, the third specifies the group ID as a number, and the last specifies a comma-separated list of users who are members of the group. For example, the bin group has group ID 2 and its members are users root, bin, and daemon. If the membership list in a line is missing (e.g., the disk group), this means that its membership is specified in the /etc/passwd file. The system administrator makes a user part of a group at the time of adding the user to the system. This group is known as a user's default group. The default group membership of a user is specified in the user's entry in the /etc/passwd file. The system administrator can make a user part of another group (in addition to his/her default group) by placing his/her username in the comma-separated list of members for the group. You can use the groups command to display which groups on your system a user is a member of. The following session shows that sarwar is a member of the faculty group only; bob belongs to the groups adm, dialout, sambashare, and courses; and davis is a member of three groups: dialout and lab.

```
$ groups sarwar
faculty
$ groups bob
faculty courses
$ groups davis
dialout lab
$
```