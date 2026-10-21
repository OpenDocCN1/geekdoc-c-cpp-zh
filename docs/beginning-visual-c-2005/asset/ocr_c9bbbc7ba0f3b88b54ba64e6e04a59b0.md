This function compares the state specified by the third argument, with a previous state that you specify in the second argument. The difference is stored in a `_CrtMemState` structure that you specify in the first argument. If the states are different, the function returns a non-zero value (true); otherwise, 0 (false) is returned.

```
void _CrtMemDumpStatistics(const _CrtMemState* state);
```

This dumps information about the free store state specified by the argument to an output stream. The state structure pointed to by the argument can be a state that you recorded using _CrtMemCheckpoint() or the difference between two states produced by _CrtMemDifference().

```
void _CrtMemDumpAllObjectsSince(const _CrtMemState* state);
```

This function dumps information on objects allocated in the free store, since the state of the free store specified by the argument; this has been recorded by an earlier call in your program to _CrtMemCheckpoint(). If you pass null to the function, it dumps information on all objects allocated since the start of execution of your program.

```
int _CrtDumpMemoryLeaks();
```

This is the function you need for the example as it checks for memory leaks and dumps information on any leak that is detected. You can call this function at any time, but a very useful mechanism can cause the function to be called automatically when your program ends. If you enable this mechanism, you get automatic detection of any memory leaks that occurred during program execution, so see how you can do that.

# Controlling Free Store Debug Operations

You control free store debug operations by setting a flag, _crtDbgFlag, which is of type int. This flag incorporates five separate control bits, including one to enable automatic memory leak checking. You specify these control bits using the following identifiers:

| Identifier | Description |
|---|---|
| `_CRTDBG_ALLOC_MEM_DF` | When this bit is on, it turns on debug allocation so the free store state can be tracked. |
| `_CRTDBG_DELAY_FREE_MEM_DF` | When this is on, it prevents memory from being freed by **delete**, so that you can determine what happens under low-memory conditions. |
| `_CRTDBG_CHECK_ALWAYS_DF` | When this is on, it causes the _CrtCheckMemory() function to be called automatically at every new and delete operation. This function verifies the integrity of the free store, checking, for example, that blocks have not been overwritten by storing values beyond the range of an array. A report is output if any defect is discovered. This slows execution but catches errors quickly. |
| `_CRTDBG_CHECK_CRT_DF` | When this is on, the memory used internally by the run-time library is tracked in debug operations. |
| `_CRTDBG_LEAK_CHECK_DF` | Causes leak checking to be performed at program exit by automatically calling _CrtDumpMemoryLeaks(). You only get output from this if your program has failed to free all the memory that it allocated. |