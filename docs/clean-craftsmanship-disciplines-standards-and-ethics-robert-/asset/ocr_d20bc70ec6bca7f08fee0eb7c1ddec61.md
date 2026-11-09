A stupid idea that works is not a stupid idea.

However, you can't leave that quick and dirty patch in place without causing harm. The longer that patch remains in the code, the more harm it can do.

Remember that the Knight Capital debacle would not have happened if the old Power Peg code had been removed from the code base. It was that old defunct code that actually made the bad trades.

What do we mean by "harm to structure"? Clearly, having thousands of global variables is a structural flaw. So is dead code left in the code base.

Structural harm is harm to the organization and content of the source code. It is anything that makes that source code hard to read, hard to understand, hard to change, or hard to reuse.

It is the responsibility of every professional software developer to know the disciplines and standards of good software structure. They should know how to refactor, how to write tests, how to recognize bad code, how to decouple designs and create appropriate architectural boundaries. They should know and apply the principles of low- and high-level design. And it is the responsibility of every senior developer to make sure that younger developers learn these things and satisfy them in the code that they write.

# ## Soft

The first word in software is *soft*. Software is supposed to be SOFT. It's supposed to be easy to change. If we didn't want it to be easy to change, we'd have called it *hardware*.

It's important to remember why software exists at all. We invented it as a means to make the behavior of machines easy to change. To the extent that our software is hard to change, we have thwarted the very reason that software exists.

Remember that software has two values. There's the value of its behavior, and then there's the value of its "softness." Our customers and users expect us to be able to change that behavior easily and without high cost.