```
```text
R1# show ppp all

Interface/ID  OPEN?  Negot?  Fail     Stage    Peer Address    Peer Name
-----------------------------------------------------------------------
Se0/0/0       LCP+   CHAP+   IPCP+    CDP>     LocalT           192.168.2.2  R2
```
```

The more obvious way to confirm that CHAP works is to use the show ppp all command, as shown at the end of Example 13-6. This command lists a single line per PPP connection in the router. The highlighted header in the example is the column where this command lists various PPP protocols and their status, with a plus sign (+) meaning that the listed protocol is OPEN, and a minus sign (–) meaning that the protocol has failed. The highlighted parts of this command in the example confirm that Serial0/0/0 uses PPP, with CHAP authentication, and that CHAP authentication worked (as proved by the OPEN status of the CHAP protocol).

# Implementing PPP PAP

PAP configuration differs from CHAP configuration in a couple of ways. First, PAP uses the similar authentication ppp pap command instead of the authentication ppp chap command. Then, PAP configures the set username/password pair much differently than CHAP. A router defines the username/password pair it will send using the ppp pap sent-username command, configured as an interface subcommand. Once sent, the other router receives that username/password pair, and compares those values with its various username password global commands. Figure 13-16 shows a completed configuration for two routers (R1 and R2), with emphasis on matching the ppp pap sent-username command on one router with the username password commands on the other router.

![](bbox=[0.068, 0.552, 0.834, 0.798])

**Figure 13-16**  *PAP Configuration*

Example 13-7 now shows two commands used to verify PAP operation. In particular, note that the show interfaces command tells us nothing more and nothing less as compared to using CHAP authentication. The line protocol status being up confirms that authentication, if configured, worked. (However, nothing in the show interfaces command output tells us whether or not CHAP or PAP has been configured.) As with CHAP, the LCP status of Open also confirms that authentication worked, again assuming that authentication is configured.