# Modeling Availability, Reliability, and Capacity with SPN

system inspection (*mit*) is assigned to transition *I*; its firing removes a token from place UI and stores one token in place UPR, under preventive maintenance. Transition *I*'s priority is one since the preventive maintenance starts, the computer stops operating; the working out stops; thus disabling F2. The mean preventive maintenance (*pmnt*) is assigned to transition *PR* (preventive maintenance). When PR fires, denoting the preventive maintenance was performed, a token is removed from place UPR and one token is stored in place W (waiting for another preventive maintenance cycle), and one token in place *RT*, which represents the release of the maintenance team.

As already mentioned, the time to failure with an increasing failure rate is dictated by the sub-net composed of places *A1* and *A2*, the timed transitions *F1* and *F2*, and immediate transitions *C1* and *C2*, their respective attributes, and for k > 1. Tokens in place *A1* and *A2* represent wear-out effects (in the case of a software subsystem, it may also encompass aging phenomenon). When preventive maintenance finishes, a token is removed from place UPR, and one is stored in place *PME* (preventive maintenance end). This enables *ATR*, and *C1* and *C2* fire if places *A1* and *A2* are respectively marked. Look at the guard expressions of *C1* and *C2*. If *A1* and *A2* have tokens, they are fireable, whereas *ATR*'s not priority is smaller than the priorities assigned to *C1* and *C2*, $\pi(C1) = \pi(C2) = 2$, and $\pi(ATR) = 1$. Firing *C1* and *C2* removes all tokens from places *A1* and *A2*, respectively. This means the system restores as new. After that, *ATR* fires and removes a token from *PME* and stores one token in place *W*, which denotes a new preventive cycle starts, and the repair team is deallocated from the preventive maintenance task by storing a token in place *RT*.

# Table 22.10 Transitions’ Attributes

| Transition | Type | W | Guard Expression |
|---|---|---|---|
| F1 | Timed | phtft | |
| F2 | Timed | 1 | |
| F3 | Immediate | 1 | |
| C1 | Immediate | 1 | (#PME = 1)AND(#A1 > 0) |
| C2 | Immediate | 1 | (#PME = 1)AND(#A2 > 0) |
| CR1 | Immediate | 1 | |
| ATR | Immediate | 1 | |
| CR2 | Timed | mttr | |
| TBPR | Timed | mtbpm | |
| TA | Immediate | 1 | |
| I | Timed | mit | |
| PR | Timed | mpmt | |