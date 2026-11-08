Routers use four different PVC status codes. A router learns about two of the possible status values, *active* and *inactive*, via LMI messages from the Frame Relay switch. The switch’s LMI message lists all DLCls for all configured PVCs on the access link and whether the PVC is currently usable (active) or not (inactive). An LMI message that lists these states means:

+   - **Active:** The Frame Relay network knows about the PVC with the listed DLCI, and the PVC is working right now.
+   - **Inactive:** The Frame Relay network knows about the PVC with the listed DLCI, and the PVC is not working right now.

Routers have two other PVC states that require a little more thought to understand. First, the static state means that the router has configured a DLCI for some PVC but the LMI is down. Because the LMI is down, the router does not know whether the PVC will work, because the router receives no LMI status messages. However, the router can at least send frames using those DLCIs and hope that the Frame Relay network can deliver them.

The other PVC state, *deleted*, means that the router configuration refers to the DLCI, but the LMI is working and lists no information about that DLCI value. The LMI status messages list status for all the PVCs defined over the access link, so this state means that the Frame Relay network does not have a definition for the PVC. Basically, this state means that the router has configured the DLCI but the switch has not.

Table I-2 summarizes the four Frame Relay PVC status codes.

# Key Topic

**Table I-2 — PVC Status Values**

| The PVC is defined to the Frame Relay network. | Active | Inactive | Deleted | Static |
|---|---|---|---|---|
| The PVC is defined to the Frame Relay network. | Yes | Yes | No | Unknown |
| The router will attempt to send frames on a VC in this state. | Yes | No | No | Yes |

As noted in the last row of the table, routers only send data over PVCs in an active or static state. Also even if the PVC is in a static state, there is no guarantee that the Frame Relay network can actually send frames over that PVC, because the static state implies that LMI is turned off and that the router has not learned any status information.

The next step in the troubleshooting process is to find the status of the PVC used to reach a particular neighbor. Continuing with the problem of R1 failing when pinging R2 (10.1.2.2), Example I-22 shows the status of the PVC with DLCI 102, as identified earlier.

# Example I-22 — show frame-relay pvc Command on R1

```
R1> show frame-relay pvc 102

PVC Statistics for interface Serial0/0/0 (Frame Relay DTE)

DLCI = 102, DLCI USAGE = LOCAL, PVC STATUS = INACTIVE, INTERFACE = Serial0/0/0.2

  input pkts 22          output pkts 193        in bytes 1256
  out bytes 16436        dropped pkts 0         in pkts dropped 0
```