```
```text
Producer writes 7 (buffer cells occupied: 2)
buffer cells:    7    5    6
                 ---  ---  ---
                        W    R

Producer writes 8 (buffer cells occupied: 3)
buffer cells:    7    8    6
                 ---  ---  ---
                            WR

Buffer is full. Producer waits.

Consumer reads 6 (buffer cells occupied: 2)
buffer cells:    7    8    6
                 ---  ---  ---
                   R        W

Producer writes 9 (buffer cells occupied: 3)
buffer cells:    7    8    9
                 ---  ---  ---
                        WR

Buffer is full. Producer waits.

Consumer reads 7 (buffer cells occupied: 2)
buffer cells:    7    8    9
                 ---  ---  ---
                   W    R

Producer writes 10 (buffer cells occupied: 3)
buffer cells:    10   8    9
                 ---  ---  ---
                            WR

Producer done producing
Terminating Producer

Consumer reads 8 (buffer cells occupied: 2)
buffer cells:    10   8    9
                 ---  ---  ---
                        W    R

Consumer reads 9 (buffer cells occupied: 1)
buffer cells:    10   8    9
                 ---  ---  ---
                        R    W

Consumer reads 10 (buffer cells occupied: 0)
buffer cells:    10   8    9
                 ---  ---  ---
                            WR

Consumer read values totaling 55
Terminating Consumer
```
```

**Fig. 17.10**  Concurrent threads manipulating a synchronized circular buffer. (Part 4 of 4.)