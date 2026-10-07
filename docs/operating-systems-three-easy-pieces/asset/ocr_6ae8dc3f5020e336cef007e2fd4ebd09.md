# HARD DISK DRIVES

The second problem is more fundamental: starvation. Imagine in our example above if there was a steady stream of requests to the inner track, where the head is currently positioned. Requests to any other tracks would then be ignored completely by a pure SSTF approach. And thus the crux of the problem:

# CRUX: HOW TO HANDLE DISK STARVATION

How we can implement SSTF-like scheduling but avoid starvation?

# Elevator (a.k.a. SCAN or C-SCAN)

The answer to this query was developed some time ago (see [CKR72] for example)

SCAN has a number of variants, all of which do about the same thing. For example, Coffman et al., introduced F-SCAN, which freezes the queue to be accessed when it is doing a sweep [CKR72]; this action places requests that come during the sweep into a queue to be serviced later.
By avoiding starvation of far-away requests, by delaying the servicing of late-arriving requests (or nearer by requests).

**C-SCAN**nC-SCAN is another common variant, short for Circular SCAN. Instead of sweeping in both directions across the disk, the algorithm only moves from outer-to-inner, and then returns to the outer track to begin again. Doing so is a bit fairer to the middle tracks, i.e., after servicing the outer track, SCAN back-and-forth passes through the middle twice before coming back to the outer track again.

For reasons that should be clear, the SCAN algorithm (and its cousins) is sometimes referred to as the *elevator* algorithm, because it behaves like an elevator which is going up or down and just not servicing requests to floors based on which floor is closer. Imagine how annoying it would be if you were going down from floor 10 to 1, somebody got on at 3 and pressed 4, and the elevator went up to 4 because it was "closer" than 1! As you can see, the elevator algorithm, when used in real life, prevents from taking place in elevators. In disks, it prevents starvation.

Unfortunately, SCAN and its cousins do not represent the best scheduling technology. In particular, SCAN (or SSTF even) does not actually adhere as closely to the principle of SJF as they could. In particular, they ignore rotation. And thus, another crux:

© 2008–19, RPACI-DUSSEAU

THREE
EASY
PIECES