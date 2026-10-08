
## 15.3.2 Breakpoints and single stepping with GDB

```
Calling testPutCallParity()
testPutCallParity() passed.

Calling testDeltaHedgingMeanPayoff()
/usr/lib/gcc/x86_64-pc-cygwin/5.3.0/include/c++/debug/vector
        :406:error:
        attempt to subscript container with out-of-bounds index
        1000, but
        container only holds 1000 elements.

Objects involved in the operation:
sequence "this" @ 0x0xffffc7a0 {
    type = NSt7__debug6vectorIsAIdEEE;
}

Breakpoint 1, 0x000000018012c574 in abort () from /usr/bin/
cygwin1.dll
(gdb) backtrace
#0  0x000000018012c574 in abort () from /usr/bin/cygwin1.dll
```

The first three lines are printed out by FMLib itself. They tell us that the function `testPutCallParity` is working fine. But that a problem has occurred in the function `testDeltaHedgingMeanPayoff`. To see this simply notice that we have a logging statement saying that `testPutCallParity` has passed, but no corresponding statement for `testDeltaHedgingMeanPayoff`.

The next error tells us that the error was detected at line `406` in a C++ file called `vector`. This doesn't mean that the bug is in the file `vector`, just that it was detected there. Since `vector` is part of the standard C++ library it is very unlikely to contain any bugs. We can guess that it is our code that is using a `vector` that is at fault.

The next lines are extremely hard to interpret and not very useful for us now. Let us ignore them and move onto the last line. This tells us that the execution has stopped at `Breakpoint 1`. This means that it has stopped because of the command `break abort` that we entered earlier. Helpfully, the last line mentions it stopped in the function `abort()`. Less helpfully, the line is also telling us which library contains the `abort` function and its memory address.

To find out more about what is happening, enter the command

```
backtrace
```

This command tells the debugger to print the current state of the stack. This is simply a list of which functions are currently running. At the bottom of the stack you will see the `main` method of the program, at the top you see the current function that is executing. Here is the printout from `backtrace` when it was run on my computer.

```
#0  0x000000018012c574 in abort () from /usr/bin/cygwin1.dll
#1  0x00000003f508a005 in cygstdc++-6!
_ZNK11__gnu_debug16_Error_formatter8_M_errorEv () from /usr/
bin/cygstdc++-6.dll
#2  0x00000001004246be in std::__debug::vector<double, std:::
allocator<double> >::operator[] (this=0xffffca0, __n=1000)
at /usr/lib/gcc/x86_64-pc-cygwin/5.3.0/include/c++/debug/
vector:406
#3  0x000000010041650f in HedgingSimulator::runSimulation (this
=0xffffcac0)
at HedgingSimulator.cpp:64
#4  0x0000000100416289 in HedgingSimulator::runSimulations (this
=0xffffcac0,
nsimulations=1) at HedgingSimulator.cpp:35
#5  0x0000000100416770 in testDeltaHedgingMeanPayoff ()
at HedgingSimulator.cpp:105
#6  0x0000000100416bd3 in testHedgingSimulator () at
HedgingSimulator.cpp:118
#7  0x0000000100402466 in main () at main.cpp:43
```

The bottom line tells us that the error occurred while the function main was executing. The error actually occurred while line 43 of main.cpp was executing. You can see this from the text at main.cpp:43.

Looking at the second line from the bottom, we can see that this line must have called testHedgingSimulator. This in turn called testDeltaHedgingMeanPayoff. Working through the stack in this way, you can see all the functions that are currently executing.

Generally speaking, the bottom of the stack doesn't reveal much about what has caused the problem. To analyse a bug, you should start at the top and work downwards until you get to the first line of code that you have written.

In the example above, line #0 is a call to the function abort(). The line #1 is hard to interpret, but what we can say is that it doesn't refer to any code we've written. Line #2 is executing line 406 of vector. Finally on line #3 we get to some code that we have written. It is line 64 of HedgingSimulator.cpp that contains the problem.

Let us look at that line of code.

```
double S = pricePath[nSteps];
```

The cause of the problem should be fairly obvious if you look at the neighbouring code. We are accessing an element of pricePath at index nSteps but in fact the price path is only nSteps long. We see that the code should actually read:

```
double S = pricePath[nSteps - 1];
```

Now that we know how to fix the bug, we should terminate the debugging session. Type **quit** to exit the debugger. You can then terminate the running process and exit the debugger.

You should now correct the code, rebuild it, and execute it again in the debugger. The code should still fail, but the stack trace should be different indicating that the bug is somewhere else.

The printout before the debugger pauses the program should now look as follows:

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_278_0.png)

All the printout except the last line is generated by our testing library. It tells us that an **ASSERT_APPROX_EQUAL** statement has failed at line 106 of **HedgingSimulator.cpp**.

If we view that code in our text editor we will see that a problem has arisen when running **testDeltaHedgingMeanPayoff**.

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_278_1.png)

We can see that we expected the PnL of the hedging simulation to be approximately zero, but in fact it was the ridiculously large number $-5.90148 \times 10^{300}$. There is clearly a mathematical error in the **runSimulations** function of our **HedgingSimulator** class. Unfortunately, in this case, if you run the **backtrace** command in **gdb** it will not provide much additional information.

To make further progress, the first thing to do is to read through the **runSimulations** code to see if there is any obvious problem. Here’s the code:

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_278_2.png)

```
std::vector<double> ret(nSimulations);
for (int i = 0; i < nSimulations; i++) {
    ret[i] = runSimulation();
}
return ret;
```

There are no actual mathematical calculations in this code, so it doesn't seem likely that this is the problem. It seems a good guess that the runSimulation method is the problem. You can see the code for this method in Figure 15.4 on page 265.

You may find it difficult to spot the bug in this code, even if you read through it line by line. The debugger can help you with this by allowing you to pause the execution at any point and print out the values of any variables you are interested in.

To do this you should quit the debugger and restart. But this time type the command

```
break HedgingSimulator::runSimulation
```

before executing the run command. This will then pause execution at the beginning of the runSimulation function.

When the program pauses you will see output similar to the following.

```
Calling testDeltaHedgingMeanPayoff()

Breakpoint 5, HedgingSimulator::runSimulation (this=0xffffc920)
    at HedgingSimulator.cpp:41
41      double T = toHedge->getMaturity();
```

This shows you that execution has paused at line 41 of HedgingSimulator.cpp. The given line of code has not yet executed. To execute it, type next.

This should have assigned a value to the local variable T. To see what value has been assigned type print T.

You can now step through the function runSimulation line by line, checking the values of the variables as you go. You should be able to confirm that there is a problem with the computation of interest in the runSimulation function that you should then be able to fix.

There is still one bug remaining in the code. Fixing it is left as an exercise.

## 15.3.3 Other commands and features

Let us briefly mention a few useful GDB features that we have not covered.

- 1. The command help can be used to find out the names of other useful commands.
- 2. The command `step` can be used to follow the execution of the code into other functions. By contrast, `next` always moves within a single function.
- 3. You can create a file called `.gdbinit` in your home area, which contains commands that should always be executed when gdb starts. A simple example file which would ensure gdb always pauses on calls to abort and on throw statements is shown below:

```
set breakpoint pending on
break abort
catch throw
```

Of course, GDB has many other interesting features that we have not covered. You should consult the documentation.

## 15.4 Other development tools and practices

A debugger is by no means the only tool you should be using to help you develop and maintain your code. In this section we will briefly review some of the important types of development tools that are available and that you should consider using.

### 15.4.1 Version control

It is essential to back up the source files of your project. It would be a disaster if we were to lose all the code for our project!

A source control system is used to keep a copy of all your source files to ensure that you never lose them. In addition, source control systems have some features that are essential for serious software development:

- (i) A history of the changes that you have made to each file. This means that if you accidentally introduce a bug, you should always have a record of what the code looked like beforehand.
- (ii) A system of labelling specific versions of your code. If you are ever going to give anyone else a copy of your software, you will want to know precisely what code they are running. By labelling each version of your source code, you can be certain what code your users are actually running.
- (iii) Tools so that different developers can work on the same project and even the same files without getting in each other’s way. Typically developers
