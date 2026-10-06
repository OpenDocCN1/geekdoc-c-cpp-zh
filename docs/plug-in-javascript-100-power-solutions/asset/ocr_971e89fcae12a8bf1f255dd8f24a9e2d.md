# Chapter 7: Chaining and Interaction 191

Note the expression passed to the While() statement is tested only at the start of each chain of calls, an entire chain will always execute before it can be stopped. If you need more precise control then you can always empty the global array CHAIN_CALLS (which contains all the items in a chain). This will stop a chain after the current statement has finished and can be done by issuing the statement CHAIN_CALLS.length = 0. If you need an even speed reaction to user input, a While() statement is not your best choice of plug-in, and you should be creating some event-driven code.

# The Plug-in

```
function While(expr, calls) {
  if (eval(expr)) {
    var temp = ''
    for (var j = 0; j < calls.length; ++j)
      temp += '' + calls[j].replace(/"\\/g, '\\\\') + '\';
    temp = temp.substr(0, temp.length)
    calls.push("While\#(InsVars('#\', Array(#2))", expr, temp))
  }
  Chain(calls)
}
```

# Pause()

There are often times during an animation when you need it to stop for a while, and can do this with the Pause() plugin. With it, you can specify a period of time in milliseconds until the next plug-in in a chain is called. In Figure 7-4, the example from the previous plug-in, While(), has a few extra commands inserted into the chain, which

Figure 7-4nInserting time delays into chains

![](bbox=[0.335, 0.666, 0.853, 0.893])