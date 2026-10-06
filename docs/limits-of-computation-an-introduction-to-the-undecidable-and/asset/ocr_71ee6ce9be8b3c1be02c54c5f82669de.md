This simple computer starts its computation with its program stored in memory (tape 3) and all its input on tape 4. The combined length of these tapes is some number I. After t steps of the program, a three-address instruction set cannot have accessed more than 3t memory locations.

At each step, the computer uses at most one new memory location. The number stored in that memory location is at most size (I + t). No result of addition, doubling, or other operation adds more than one digit to a number in base 2. Thus, after t steps, the contents of tape t have length bounded by Kt².

This means a one-time-unit random access to memory can be emulated by the Turing machine in Kt²; thus t steps can be emulated in Kt³.

Now, recall that a multitape Turing machine can be emulated by a single-tape Turing machine, and the order is by most squared. Thus, the simple computer can be emulated by a standard Turing machine in K’t—and importantly, what is polynomial on this computer is still polynomial on a standard Turing machine.

# 5.6 ENCODINGS OF TURING MACHINES

For many uses of Turing machines, we want to encode them (and their inputs) into some standard alphabet. There are several reasons to do this. First, we are writing Turing machines for different problems. This is not efficient; we do not build different computers for different problems; rather, we write different programs that run on the same computer. Second, we want a (relatively) short and machine-readable description of a Turing machine—something more standard and concise than the rather long English descriptions or complicated diagrams we have been writing.

In computer science, this alphabet is most naturally Σ = {0, 1}. To use only two characters, one of the characters must be a separator. Thus, all information must be encoded as strings of 0’s; we will need to use the 1 as a separator character (or, of course, vice versa).

One problem is to encode the alphabet of the Turing machine. If all alphabets are subsets of some standard alphabet such as the ASCII or Unicode sets of characters, there would be less of a problem, since each character in any alphabet could be encoded in Unicode. In this sense, all “regular” characters have already been coded into the alphabet of {0,1}. But there is no restriction on the alphabets of formal languages requiring them to use any symbol already in existence anywhere.