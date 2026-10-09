This leaves the stack storing:

```
push  return C
push  return B
push  return A
push  return main
```

When function D finishes it pops the return address off the top of the stack, i.e. it returns C. When C finishes it pops its return address from the new top of the stack, i.e. it returns B

```
push  return B
push  return A
push  return main
```

and so on.

You can see that if we follow the rule “push the return address on the stack when the function is called and pop the return address off the top of the stack when the function is finished” everything just works.

A stack follows the natural call and return flow of the function.

When this was noticed the stack became the standard way to implement functions.

Today we use a stack to implement functions, but before this the return address was handled in an ad-hoc way. Often, a single location was used to store the return address and this resulted in the restriction that you could only call a function which in turn could not call a subsequent function. Function calls were restricted to a depth of one. Later additional return variables were added, but you were still restricted in the depth of function calls you could implement and it wasn’t particularly efficient.

# Automatic Local Variables

For some time, the stack was used just for the return address of functions. In those early days any variables that you created within a function had the same status as variables created in the “main” program. That is, when you used a variable in a function it became a top-level global variable which could be accessed from everywhere in the program. This made getting results out of a function easy, but it also made programming very error-prone because you couldn’t write a function in isolation – you had to avoid variable names that were used elsewhere in the program.

Then someone noticed that the stack could be used to create variables that were automatically local to the function. This approach was made clear in the 1950s as part of the Algol language, but it took longer for other languages to adopt it.