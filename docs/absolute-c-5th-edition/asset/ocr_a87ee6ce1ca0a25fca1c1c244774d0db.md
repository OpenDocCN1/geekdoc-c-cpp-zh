# Recursive void Functions 583

computer turns its attention to the top sheet of paper on the stack. This sheet contains the partially completed computation that is waiting for the recursive computation that just ended. Thus, it is possible to proceed with suspended computation. When suspended computation ends, the computer discards that sheet of paper and the suspended computation that is below it becomes the computation on top of the stack. The computer turns its attention to the suspended computation that is now on top of the stack, and so forth. The process continues until the computation on the bottom sheet is completed. Depending on how many recursive calls are made and how the function is written, the stack may grow and shrink in any fashion. Note that the sheet in the stack can only be accessed in a last-in/first-out fashion, but that is exactly what is needed to keep track of recursive calls. Each suspended version is waiting for the completion of the version directly above on the stack.

Needless to say, computers do not have stacks of paper. This is just an analogy. The computer uses portions of memory rather than pieces of paper. The content of one of these portions ("sheets of paper") is called an activation frame. These activation frames are handled in the last-in/first-out manner just discussed. These activation frames do not contain a single copy of the function definition. However, merely reference enough information to allow the computer to act as the activation frame contained a complete copy of the function definition.

activation frame

Stack
A stack is a last-in/first-out memory structure. The first item referenced or removed from a stack is always the last item entered into the stack. Stacks are used by computers to keep track of recursion (and for other purposes).

# PITFALL: Stack Overflow

There is always some limit to the size of the stack. If there is a long chain in which a function makes a recursive call to itself, and that call results in another recursive call, and that call produces another recursive call, and so forth, then each recursive call in chain will cause another activation frame to be placed on the stack. If this chain is too long, the stack will grow beyond its limit. This is an error condition known as a stack overflow. If you receive an error message that says "stack overflow," it is likely that some function call has produced an excessively long chain of recursive calls. One common cause of stack overflow is infinite recursion. If a function is recursing infinitely, then it will eventually try to make the stack exceed any stack size limit.

stack overflow

![](bbox=[0.113, 0.653, 0.183, 0.683])