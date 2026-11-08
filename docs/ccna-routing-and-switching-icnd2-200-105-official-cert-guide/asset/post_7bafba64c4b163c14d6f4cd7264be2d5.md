
The first of these problems—a mismatch between the configured data link protocols—is easy to identify and fix. The **show interfaces** command lists the encapsulation type on about the seventh line of the output, so using this command on both routers can quickly identify the problem. Alternatively, a quick look at the configuration, plus remembering that HDLC is the default serial encapsulation, can confirm whether the encapsulations are mismatched. The solution is simple: Reconfigure one of the two routers to match the other router's **encapsulation** command.

The other two root causes require a little more discussion to understand the issue and determine if they are the real root cause. The next two sections take a closer look at each.

## Keepalive Failure

The router **keepalive** feature helps a router notice when a link is no longer functioning. Once a router believes the link no longer works, the router can bring down the interface, allowing the routing protocol to converge to use other routes if they exist.

The keepalive function on an interface causes routers to send keepalive messages to each other every keepalive interval, defaulting to 10 seconds. For instance, on a serial link between R1 and R2, R1 sends a keepalive message every 10 seconds, and R2 expects to receive those keepalive messages every 10 seconds. If R2 fails to receive the keepalive messages for a set number of consecutive keepalive intervals (usually three or five intervals), R2 believes R1 has failed, and R2 changes the link to an up/down state. The keepalive process happens in both directions as well—R1 sends keepalives with R2 expecting to receive them, and R2 sends keepalives with R1 expecting to receive them.

A keepalive mismatch occurs when one router has keepalives enabled and one router does not. That combination is a mistake, and should not be used. Note that this keepalive mismatch mistake only breaks HDLC links; the PPP keepalive feature prevents the problem. Figure 13-23 shows one such example with HDLC and with R1 mistakenly disabling keepalives.

![](img/79473ea15699e01619d2aa789f5bd43b_410_0.png)

**Figure 13-23** *Results when Using HDLC with a Keepalive Mismatch*

Note that the router interface that disables keepalives remains in an up/up state. In the scenario shown in Figure 13-23, R2's interface fails because

- R1 does not send keepalive messages, because keepalives are disabled.
- R2 still expects to receive keepalive messages, because keepalives are enabled.

You can verify the keepalive setting by looking at the configuration or by using the **show interfaces** command. The examples in this chapter list several examples of the **show interfaces** command that happen to list the text "Keepalive set (10 second)," meaning that keepalives are enabled with a 10-second interval. R1 would list the text "Keepalive not set" in this case.

## PAP and CHAP Authentication Failure

As mentioned earlier, a failure in the PAP/CHAP authentication process results in both router interfaces failing to an up/down state. As shown in Examples 13-6 and 13-7, you can use the **show interfaces** and **show ppp all** commands to look further into the status of the PPP authentication process. By doing so, you can isolate and discover the root cause of why the interface is in an up/down state, ruling out or ruling in PPP authentication as the root cause.

Another deeper method to troubleshoot PPP authentication problems uses the **debug ppp authentication** command.

CHAP uses a three-message exchange, as shown back in Figure 13-14, with a set of messages flowing for authentication in each direction by default. If you enable the debug, shut down the link, and bring it back up, you will see debug messages that match that three-way exchange. If authentication fails, you see a failure message at the point at which the process fails, which may help you decide what specifically needs to be fixed.

Example 13-10 shows the three related debug messages when a link comes up. The network connects R1's S0/0/0 to router R2. The example extracts the three related debug messages from what would be a few dozen debug messages, so you would have to look for these. However, the output highlights the important parts of the process as seen back in Figure 13-14, as follows:

1. The "O" refers to output, meaning that this local router, R1, has output (sent) a Challenge message. Note the "from R1" at the end of the debug message, stating who the message is from.
2. The "I" refers to input, meaning that this local router, R1, has input (received) a Response message. Note the "from R2" at the end of the line.
3. The "O FAILURE" refers to R1 sending out a Failure message, telling R2 that the authentication process failed.

**Example 13-10** *Debug Messages on Router R1 Confirming the Failure of CHAP*

```
R1# debug ppp authentication
PPP authentication debugging is on
! Lines omitted for brevity
*Nov 18 23:45:48.820: Se0/0/0 CHAP: O CHALLENGE id 1 len 23 from "R1"
*Nov 18 23:45:48.820: Se0/0/0 CHAP: I RESPONSE id 1 len 23 from "R2"
*Nov 18 23:45:48.820: Se0/0/0 CHAP: O FAILURE id 1 len 25 msg is "Authentication failed"
```

While using a debug command may tell us something about the problem, it does not always point to the specific command that is misconfigured. In this case, the fact that both routers send at least one CHAP message implies that both router interfaces can send frames, and that they have enabled CHAP. It looks more like R1 has rejected the hashed password supplied by R2. Note that this example was built by changing the **username** command to have an incorrect password, so that the CHAP process worked but the authentication was rejected.

## Review All the Key Topics

Table 13-9  Key Topics for Chapter 13

| Key Topic Element | Description | Page Number |
| --- | --- | --- |
| Table 13-3 | Speeds for WAN links per the T-carrier system | 334 |
| Figure 13-7 | Role of the CSU/DSU and the router as DCE and DTE | 335 |
| List | PPP features | 340 |
| List | Comparison of PPP LCP and NCP | 341 |
| Figure 13-13 | Example of messages sent by PAP | 342 |
| Figure 13-14 | Example of messages sent by CHAP | 343 |
| Figure 13-16 | Sample PAP configuration | 346 |
| List | MLPPP major configuration concepts | 349 |
| Figure 13-21 | Sample MLPPP configuration | 350 |

## Key Terms You Should Know

leased line, telco, serial link, WAN link, T1, DS0, DS1, T3, customer premises equipment, CSU/DSU, serial cable, DCE, DTE, HDLC, PPP, CHAP, PAP, IP Control Protocol, keep-alive, Link Control Protocol, Multilink PPP

## Command References

Tables 13-10 and 13-11 list configuration and verification commands used in this chapter. As an easy review exercise, cover the left column in a table, read the right column, and try to recall the command without looking. Then repeat the exercise, covering the right column, and try to recall what the command does.

Table 13-10  Chapter 13 Configuration Command Reference

| Command | Description |
| --- | --- |
| encapsulation [hdlc \| ppp] | Interface subcommand that defines the serial data-link protocol |
| [no] shutdown | Administratively disables (shutdown) or enables (no shutdown) the interface in whose mode the command is issued |
| clock rate speed | Serial interface subcommand that, when used on an interface with a DCE cable, sets the clock speed in bps |
| bandwidth speed-kbps | Interface subcommand that sets the router's opinion of the link speed, in kilobits per second, but has no effect on the actual speed |
| description text | Interface subcommand that can set a text description of the interface |
| ppp authentication [pap \| chap] | Interface subcommand that enables only PAP or only CHAP authentication |
| username name password secret | Global command that sets the password that this router expects to use when authenticating the router with the listed hostname |
| ppp pap sent-username name password secret | Interface subcommand that defines the username/password pair sent over this link when using PAP authentication |
