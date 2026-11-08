Figure 6-6 shows with this command, it lists multiple authentication methods. The switch tries the first method, and if that method returns a definitive answer, the process is done. However, if that method is not available (for instance, none of the AAA servers is reachable over the IP network), IOS on the local device moves on to the next method.

```
aaa authentication login default <method 1> <method 2>
                 ^           ^
                 |           |
          Tries This First   |
                      Tries This Second
```

**Figure 6-6** *Default Login Authentication Rules*

The idea of defining at least a couple of methods for login authentication makes good sense. For instance, the first method could be a AAA group so that each engineer logs in to each device with that engineer's unique username and password. However, you would not want the engineer to fail to log in just because the IP network is having problems and the AAA servers cannot send packets back to the switch. So, using a backup login method (a second method listed in the command) makes good sense.

Figure 6-7 shows three sample commands for perspective. All three commands reference the same AAA group (WO-AAA-Group). The command labeled with a 1 in the figure takes a shortsighted approach, using only one authentication method with the AAA group. Command 2 in the figure uses two authentication methods: one with AAA and a second method (local). (This command's local keyword refers to the list of local **username** commands as configured on the local switch.) Command 3 in the figure again uses a AAA group as the first method, followed by the keyword login, which tells IOS to use the **password** line subcommand.

+   1. aaa authentication login default `group WO-AAA-Group`
+      (Uses AAA Server)
+   2. aaa authentication login default `group WO-AAA-Group` `local`
+      (Uses AAA Server)
+      2nd: Uses Local Usernames
+   3. aaa authentication login default `group WO-AAA-Group` `login`
+      (Uses AAA Server)
+      2nd: Use Login Password

**Figure 6-7** *Examples of AAA Login Authentication Method Combinations*

# ## DHCP Snooping

To understand the kinds of risks that exist in modern networks, you have to first understand the rules. Then you have to think about how an attacker might take advantage of those rules in different ways. Some attacks might cause harm, and might be called a denial-of-service (DoS) attack. Or an attacker may gather more data to prepare for some other attack. Whatever the goal, for every protocol and function you learn in networking, there are possible methods to take advantage of those features to give an attacker an advantage.