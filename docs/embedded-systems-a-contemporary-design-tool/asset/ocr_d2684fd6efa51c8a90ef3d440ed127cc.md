# 9.19.5.1 The Logic Circuit

The logic circuit is a physical device that realizes a Boolean function. The logic circuit can be modeled as a directed acyclic graph, as shown in Figure 9.38.

![](bbox=[0.263, 0.166, 0.363, 0.236])

E = Dr(A + B) Figure 9.38 Logic Gate MOC

# 9.19.5.2 The Random Access Machine – RAM

The Random Access Machine – RAM MOC is modeled as two FSMs: RAM-CPU and RAM as shown in the diagram is shown in Figure 9.39.

![](bbox=[0.263, 0.382, 0.773, 0.532])

Figure 9.39 CPU-RAM MOC

The RAM component holds N words, each identified by an address. It has one output word: outword and three input words: cmd, read, and write.

+   - cmd: read, write, nop
+   - read: outword ← data @ adx
+   - write: data@adx ← inword

The RAM-CPU component comprises a CPU that implements a fetch and execute cycle as it alternately reads an instruction from RAM and executes it. The RAM MOC is similar to the Turing machine but supports random access.

# 9.19.5.3 The Turing Machine

The basic Turing Machine is a hypothetical computing device formulated by the British mathematician Alan Turing. The machine is capable of simulating any computer algorithm. The system comprises a program that drives a read-write head. The head interfaces to a tape and under the control of the program, it can read from or write to the tape and move to the left or the right, i.e. make a state change. The Basic Turing machine is shown in the diagram in Figure 9.40.