left of this bit pair). Note that this addition will be in the ternary number system, and the multiplying factor four is to adjust the weight of T with respect to the currently scanned bit bit pair. Also, since this addition will be in the ternary number system, the weight of four can be assigned to T by adding the two ternary numbers T0 and 0T. Thus, the equivalent ternary representation of the part of the binary message from its msb to the currently scanned bit pair will then be obtained as T0 \(\oplus\) 0T \(\oplus\) x, where \(\oplus\) represents a ternary addition operator and x is the ternary number equal to 0, 1, or 2 (when the scanned bit pair is 00, 01 or 10, respectively), or equal to (10)3 (when the scanned bit pair is 11).

**Example 33.** _Consider the binary number_ 10011100_. First, we get T_=2 _from the leftmost two bits_ 10_. Then, for the next two bits, the equivalent ternary digit is_ 1_. We add (in ternary) the three numbers_ (20)3_,_ (02)3 _and_ (1)3 _to get the changed value of T_=(_100_)3 _(which is equal to_ 9 _in decimal corresponding to the binary digits_ 1001 _scanned so far). For the next two bits, we get the equivalent ternary representation as_ (_10_)3_, which is added to_ (1000)3_(= T0) and_ (0100)3_(= 0T) in ternary to get the changed value of T_=(_1110_)3_=_(39)10_. Finally, for the bit pair_ 00_, we add_ (_11100_)3 _to_ (01110)3 _to get the equivalent ternary number as_ (_12210_)3_=_(156)10_._

The _Binary2Ternary_ algorithm outlines the steps required to convert a number from binary to ternary.

+   1: **procedure** BINARY2TERNARY(IN bit vector _B_, integer _n_, OUT ternary number _T_)
+   2: _/_** Initialization **/\_
+   3: **if** _bn_-1_bn_-2=00 **then**
+   4: _T_ \(\leftarrow\) 0;
+   5: **end if**
+   6: **if** _bn_-1_bn_-2=01 **then**
+   7: _T_ \(\leftarrow\) 1;

© 2016 by Taylor & Francis Group, LLC