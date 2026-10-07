# CONDITION VARIABLES

| Tc1 | State | Tc2 | State | Tp | State | Count | Comment |
|---|---|---|---|---|---|---||
| c1 | Run | | Ready | Ready | 0 | |
| c2 | Run | | Ready | Ready | 0 | |
| c3 | Sleep | | Ready | Ready | 0 | Nothing to get |
| | Sleep | | p1 | Run | 0 | |
| | Sleep | | p4 | Run | 1 | Buffer now full |
| | Ready | | p5 | Run | 1 | Tc1 awoken |
| | Ready | | p6 | Run | 1 | |
| | Ready | | p1 | Run | 1 | |
| | Ready | | p2 | Run | 1 | |
| | Ready | | p3 | Sleep | 1 | Buffer full; sleep |
| | Ready | c1 | | Sleep | 1 | Tc2 sneaks in... |
| | Ready | c2 | | Sleep | 1 | |
| | Ready | c4 | | Sleep | 0 | ... and grabs data |
| | Ready | c5 | | Ready | 0 | Tp awoken |
| | Ready | c6 | | Ready | 0 | |
| c4 | Run | | Ready | 0 | Oh oh! No data |

Figure 30.9: Thread Trace: Solution (v1)

buffers are full (p2), and finding that not to be the case, goes ahead and fills the buffer (p4). The producer then signals that a buffer has been filled (p5). Critically, this moves the first consumer (Tc1) from sleeping on a condition variable to the ready queue; Tc1 is now able to run (but not yet running). The producer then continues until realizing the buffer is full, at which point it sleeps (p6, p1–p3).

Here is where the problem arises: another occurs (Tc2) sneaks in and consumes the only existing value in the buffer (c1, c2, c4, c5, c6, skipping the wait at c3 because the buffer is full); just Assume Tc1 runs before returning the wait, it re-acquires the lock and returns. Then it gets (1), but there are no buffers to consume! An assertion, have somehow inserted Tc1 from trying to consume because Tc2 snuck and consumed the only value in the buffer that had been produced. Figure 30.9 shows the chain effect takes, as well as its scheduler state (Ready, Running, or Sleeping) over time.

The problem arises for a simple reason: after the producer wakes Tc1, but before Tc1 runs, the state of the buffer buffer changed (thanks to Tc2). Signaling a thread wakes them up; thus is a hint that the state of the world has changed (in this case, a value has been placed in the buffer), but there is no guarantee that when the woken runs, the state will still be as desired. This interpretation of what a signal means is often referred as Mesa semantics, after the first research that built a condition variable in such a manner [LR80]; the contrast, referred to as

© 2008–19, ARPACI-DUSSEAU

THREE
EASY
PIECES