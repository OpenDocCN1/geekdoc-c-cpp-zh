# # Code for CPUs

There are a huge variety of programming languages out there, but one thing almost all of them have in common is that they are based on the English language. Even if you don't know a programming language you can usually look at some simple code in that language and work out roughly what it is doing.

![](bbox=[0.014, 0.302, 0.252, 0.981])

# ## Machine code

Computers, though, don't understand English. When they run a program they need it to be translated into machine code, instructions that their Central Processing Unit (CPU) understands. Machine code contains a very limited set of instructions that correspond to actual operations hardwired into the CPU.

The very first computers were programmed directly in machine code but this was extremely tricky work: programmers had to calculate a very precise set of values on every line to instruct the CPU what to do. Worse, every type of CPU had its own different machine code, so a program had to be rewritten from scratch to run on another type of computer.

Here's an example of some machine code:

```
~~~
77
29 20 b3
61 9e
70
0c b7 f6
~~~
```