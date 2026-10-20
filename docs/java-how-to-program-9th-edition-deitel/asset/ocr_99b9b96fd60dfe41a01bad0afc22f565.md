```
Consumer reads 1 (buffer cells occupied: 0)
buffer cells:    1   -1   -1
            ---  ---  ---
                 WR

Buffer is empty. Consumer waits.
Producer writes 2 (buffer cells occupied: 1)
buffer cells:    1    2   -1
            ---  ---  ---
                 R   W

Consumer reads 2 (buffer cells occupied: 0)
buffer cells:    1    2   -1
            ---  ---  ---
                     WR

Producer writes 3 (buffer cells occupied: 1)
buffer cells:    1    2    3
            ---  ---  ---
            W          R

Consumer reads 3 (buffer cells occupied: 0)
buffer cells:    1    2    3
            ---  ---  ---
            WR

Producer writes 4 (buffer cells occupied: 1)
buffer cells:    4    2    3
            ---  ---  ---
            R   W

Producer writes 5 (buffer cells occupied: 2)
buffer cells:    4    5    3
            ---  ---  ---
            R        W

Consumer reads 4 (buffer cells occupied: 1)
buffer cells:    4    5    3
            ---  ---  ---
                 R   W

Producer writes 6 (buffer cells occupied: 2)
buffer cells:    4    5    6
            ---  ---  ---
            W   R

Producer writes 7 (buffer cells occupied: 3)
buffer cells:    7    5    6
            ---  ---  ---
                 WR

Consumer reads 5 (buffer cells occupied: 2)
buffer cells:    7    5    6
            ---  ---  ---
                 W   R

Producer writes 8 (buffer cells occupied: 3)
buffer cells:    7    8    6
            ---  ---  ---
                     WR
```