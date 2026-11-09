**FIGURE 4-2** A thread’s stack with the M1 method about to be called.

All but the simplest of methods contain some **prologue code**, which initializes a method before it can start doing its work. These methods also contain **epilogue code**, which cleans up a method after it has performed its work so that it can return to its caller. When the M1 method starts to execute, its prologue code allocates memory for the local name variable from the thread’s stack (see Figure 4-3).

![](bbox=[0.126, 0.211, 0.564, 0.392])

**FIGURE 4-3** Allocating M1’s local variable on the thread’s stack.

Then, M1 calls the M2 method, passing in the name local variable as an argument. This causes the address in the name local variable to be pushed on the stack (see Figure 4-4). Inside the M2 method, the stack location will be identified using the parameter variable named s. (Note that some architectures pass arguments via registers to improve performance, but this distinction is not important for this discussion.) Also, when a method is called, the address indicating where the called method should return to in the calling method is pushed on the stack (also shown in Figure 4-4).

![](bbox=[0.126, 0.579, 0.564, 0.816])

**FIGURE 4-4** M1 pushes arguments and the return address on the thread’s stack when calling M2.

When the M2 method starts to execute, its prologue code allocates memory for the local length and tally variables from the thread’s stack (see Figure 4-5). Then the code inside method M2 executes. Eventually, M2 gets to its return statement, which causes the CPU’s instruction pointer to be