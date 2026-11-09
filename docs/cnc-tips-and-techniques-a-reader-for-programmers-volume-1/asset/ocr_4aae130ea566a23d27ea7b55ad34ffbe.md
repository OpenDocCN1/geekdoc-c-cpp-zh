This is nothing more than a retract clearance controlled by the programmer and is usually very small: 0.5–1.0 mm or 0.02–0.04”.

The second block is identical to both cycles. The addresses P and Q always go together. The *address P* identifies the block number representing the tool position at the contour start, and the *address Q* identifies the block number representing tool position at the *contour end*. Both block numbers must be unique (not duplicated in the program).

Addresses U and W also work together; they represent the stock allowance left for subsequent finishing. The *U-address* is the amount of stock left on *diameter*, and the *W-address* is the amount of stock left of *faces*. For simultaneous XZ motions, the U and W stock allowances will be compounded by the control system. Note that U is a dimension on diameter — a 0.03” physical stock will be programmed as U0.06. A positive amount of U or W leaves stock on the positive side of the contour; a negative amount leaves the stock on the negative side of the contour, determined by the cutting direction. For the majority of work, the U-address will be positive for turning, and negative for boring. A W-address is typically positive for both types of operations, but it could be negative, for example, in some back-boring operations.

The *F-address* is the cutting feedrate and the *S-address* is the cutting speed, normally in G96 mode (constant cutting speed), programmed in *feet per minute* or *meters per minute*. If the speed has been programmed at the program beginning, it is not necessary to include it in the cycle call.

# The G70 Cycle

Finishing cycle G70 is always programmed as a one-block command, with the mandatory P and Q, and optional F and S data:

```
G70 P.. Q.. F.. S..
```