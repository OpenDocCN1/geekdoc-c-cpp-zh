```
def forestSize[A](forest: Forest[A]): Int = forest match
  case Nil          => 0
  case tree :: trees => treeSize(tree) + forestSize(trees)
```

Listing 6.8: Recursive implementation of size on N-ary trees.

These functions are mutually recursive: treeSize calls forestSize, and forestSize calls treeSize. N-ary trees are explored as a case study in Chapter 11.

# 6.5 Tail Recursion

Function invocation is typically implemented in terms of an execution stack. When you invoke a function, a new stack frame is allocated and pushed on the execution stack. The frame contains, among other things, the function’s arguments and space for its local variables. It is popped from the stack when control returns from the call.

Recall that recursion was introduced as a mechanism that can nest function calls arbitrarily—it was used to replace a useless repetition f(x); f(x); f(x) with a more useful f(f(f(x))). In the same way that loops can involve many repetitions, functions can involve many recursive calls. As a result, recursive code often leads to heavy usage of the execution stack. In particular, a deeply recursive function can fail to evaluate because it runs out of stack space.

Compilers of functional programming languages often optimize stack usage by focusing on tail calls. A tail call is a function call that takes place at the very end of another function, as in the following pattern:

```
function f(x,y,z) {
  <code>
  return g(t,u,v)
}
```

In this pattern, when control returns from the call to g, it will then immediately return from the call to f—function f has nothing to do after the call to g. In particular, by the time function f initiates its call to function g, its x, y, and z arguments are no longer needed (and neither are its local variables). They can be popped from the stack before branching into g, thus limiting stack growth—pop a frame, then push a frame. Furthermore, if the call is a recursive call (f and g are the same function), the whole stack frame can be reused by reassigning variables x, y, and z to have the values t, u, and v, and then branching back to the beginning of f. In that case, you can execute the computation as a loop, without using any stack at all.

Some functional languages may guarantee that some or all tail calls are optimized, while others might focus solely on tail recursive calls, and still others might leave the decision to specific compiler implementations. Hybrid languages, in which functions are implemented in terms of methods, tend to face a more challenging situation, since method invocation typically involves its own unique characteristics (see the discussion of dynamic dispatching in Section 15.7).