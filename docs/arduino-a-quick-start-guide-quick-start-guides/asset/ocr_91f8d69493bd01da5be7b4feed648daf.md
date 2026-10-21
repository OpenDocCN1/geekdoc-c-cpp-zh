![](bbox=[0.05, 0.05, 0.95, 0.32])

# Figure 8.6: Two Ethernet shields for the Arduino

Hardware is only one aspect of turning an Arduino into a network device. We also need some software for network communication. The Arduino IDE comes with a convenient Ethernet library that contains a few classes related to networking. We will use it now to access a DAYTIME service on the Internet.

A DAYTIME service⁹ returns the current date and time as an ASCII string. DAYTIME servers listen on either TCP or UDP port 13. You can find many DAYTIME services on the Internet; one of them runs at time.nist.gov. Before we use the service programmatically with an Arduino, see how it works using the telnet command:

```
maik> telnet time.nist.gov 13
Trying 192.43.244.18...
Connected to time.nist.gov.
Escape character is '^[A'].
55480 10-10-11 13:25:35 28 0 0 138.5 UTC(NIST) *
Connection closed by foreign host.
```

> 9. http://en.wikipedia.org/wiki/DAYTIME