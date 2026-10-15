named jitviawindbg and the entity I want to look up is the Add method of the Program class. Note that this command confirms that our Add method has not yet been converted from IL into machine code.

```
0:001> |sos.name2ee jitviawindbg Program.Add
Module:             00007ffd565e2870
Assembly:           jitviawindbg.dll
Token:              0000000006000002
MethodDesc:         00007ffd565e49d0
Name:               Program.Add(Int32, Int32)
JIT:                Not JITTED yet. Use !bpmd -md 00007FFD565E49D0 to break on run.
0:001> !sos.u 00007ffd565e49d0
Not jitted yet
```

Additionally, if I attempt to use the SOS command to unassemble or inspect the machine code for the Add method, it will also tell me that the add method has not yet been jitted, so it cannot convert the machine code for that method back into it's more readable assembly language view. However, if JIT compilation is working the way I said it does, we should expect that the next time we use the same command, which will be after the call to add has occurred and theoretically triggered compilation, that we will see something different. Similarly, if I unassemble our main method, we can see two things. First, main itself has already been compiled, which makes sense since we're currently paused within main on its first call to console.readline. And second, we can see the call to our Add method from within main.