![](bbox=[0.191, 0.091, 0.882, 0.539])

The numbers to the right of each `?` in the preceding dialog represent the SML program instructions input by the user. The SML program has now been placed (or loaded) into built-in array `memory`. Now the Simpletron executes your SML program. Execution begins with the instruction in location `00` and, like C++, continues sequentially, unless directed to another part of the program by a transfer of control.

Use variable `accumulator` to represent the accumulator register. Use variable `instruction-counter` to keep track of the location in memory that contains the instruction being performed. Use variable `operationCode` to indicate the operation currently being