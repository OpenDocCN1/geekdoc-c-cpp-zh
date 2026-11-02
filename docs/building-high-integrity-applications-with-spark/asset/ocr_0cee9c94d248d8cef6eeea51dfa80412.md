access hardware registers through ordinary variables. In Ada, memory mapped variables are defined by the Volatile and Address aspects. With the addition of SPARK aspects describing the external properties of memory mapped variables, we can use the SPARK tools to analyze the program’s use of these variables.

If the external subsystem reads the value of a memory mapped variable at a time of its own choosing, that variable is said to have an *asynchronous reader*. Similarly, if the external subsystem updates a variable at a time of its own choosing, that variable is said to have an *asynchronous writer*. Notice that the terms asynchronous reader and asynchronous writer are from the point of view of the external subsystem. It is the external subsystem that is reading and writing.

SPARK provides two Boolean aspects to specify either or both of these possibilities:

+   - **Async_Readers:** Any object for which Async_Readers is true may be read at any time (asynchronously) by hardware or software outside the program.
+   - **Async_Writers:** Any object for which Async_Writers is true may be changed at any time (asynchronously) by hardware or software outside the program.

Async_Readers has no effect on either flow analysis or proof analysis and thus serves mostly a documentation purpose. Async_Writers has no effect on flow analysis but does have an effect on proof analysis. The proof tool takes into account that two successive reads of the same variable may return different results.

SPARK provides two related Boolean aspects that do control the flow analysis of external objects:

+   - **Effective_Reads:** Indicates that the program’s reading the value of a volatile variable has an effect on the external hardware or software subsystem. Effective_Reads can only be specified on a variable that also has Async_Writers set.
+   - **Effective_Writes:** Indicates that the program’s assigning a value to the variable has an effect on the external hardware or software subsystem. Effective_Writes can only be specified on a variable that also has Async_Readers set.

Both Effective_Reads and Effective_Writes have an effect on flow dependencies. Reading the former or writing the latter is modeled as having an effect on the value of the variable.

We typically set Effective_Reads to true for devices that provide a stream of input values such as mass storage devices and serial ports and to false for