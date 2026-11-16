# Message Encryption

In many online games, not all the messages need highly secured encryption, and due to performance issues, only a few types of communicated messages are made secure.

When we add an encryption option to our IDL grammar, and IDL output code pattern and encryption facilities to our streaming class, we can make use of encryption easily just with one definition such as:

```
[encrypted] RequestLogin(string id, string password);
```

# Message Compression

Message compression is easily implemented by enhancing our streaming class and our IDL grammar. For example, we may want to add a "number of bits" option for each parameter, which we can define like this:

```
Knight_Attack(int type:4,int magicBuff:7,int critical:1);
```

Variable type takes four bits and magicBuff takes seven bits, while critical takes one bit. Of course, we would then need to modify our streaming class for bitwise manipulation.

# Switch-Case Optimization

For better performance, it is also a good approach to substitute switch-cases in RPC stub to a binary search tree, to get O(logn) for n as number of RPC functions.

# Debugging and Profiling Tools

It may be easier to profile servers by adding some probe code to the RPC proxy and stub code templates. For example, when we want to trace every incoming or outgoing message, we can do so just by adding code that prints the function name and parameter values to console or debug output. Of course, we can also view the trace log records showing what functions and parameters have been passed. This is a great way to help detect vulgarity received from a bad game client or RPC body functions that cause long process times.

# Synchronous RPC

Most games will typically not require synchronous RPC; however, if it is needed for your programs, you can add this faculty to your RPC at runtime.

Adding synchronous RPC to our example requires some more work:

+   - We need to define more sequences that wait until the RPC body returns and passes the return values to the RPC function caller.
+   - Only guaranteed messages are acceptable with synchronous RPC.
+   - We need to add a parameter direction option, which are input parameters (inparam) and output parameters (outparam). Inparam is sent to the RPC server