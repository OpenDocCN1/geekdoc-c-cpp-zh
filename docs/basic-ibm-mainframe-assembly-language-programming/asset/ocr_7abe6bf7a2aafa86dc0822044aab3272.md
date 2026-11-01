addresses if they are to be accessed by Load and Store instructions, the initial byte of the table must, therefore, be on a full word boundary. As the table one line 121 is declared with a C data type code, there is no guarantee that the first byte will on a full word boundary. The data type code C has no alignment requirement.

However, we are assured that the table does, in fact, begin on a full word boundary because of the declaration on line 116. The notation 0F in a DS statement causes the assembler to allocate zero instances of a full word binary. That is, nothing. But this has the side effect of forcing the location counter to advance to the next full word boundary (an address value evenly divisible by 4). Since there is nothing allocated by the DS on line 116, this is the byte on which the table begins. Thus the table TAB begins on a full word boundary.

In our program, entries in the table will be accessed as offsets from a register. The word entry will be at zero bytes from the register and the count at eight bytes from the register. The next entry will be at 12 bytes from the register.

Note that the table TAB on line 121 is the last declared field in the program and that the LTORG appears prior to TAB. The LTORG causes any literals, such as =F'100', to be placed in memory beginning at the point where the LTORG appears. Thus, all literals will appear prior to our definition of TAB.

Why is it important to place the literals prior to the TAB declaration? Since the extent of TAB is much larger than 4095, the largest displacement allowed in ordinary RX, RS, SS, and SI instructions, anything placed after TAB would be out of using in a program with a single base register. We could have more than one base register, but it is unnecessary. We only need that the first byte of TAB be within using so that we can load the address of this initial byte into a register. After that, all table addressing will be relative to this register.

The program works as follows:

+   1. Input consists of lines of text up to 80 characters long. Input lines are processed in a loop beginning at line 7 and extending through line 62. Input is read into the field IN on line 7 and a branch is made to EOF when there is no more data (line 8).
+   2. Each input line is processed by a Translate (TR) instruction to remove punctuation (except the hyphen and single quote characters) and numerics. The TR converts all alphabetics to upper case (a common case for indexing terms is normally used in retrieval applications).