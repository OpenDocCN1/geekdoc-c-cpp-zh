# Chapter 40. Atomics

# 288

And we've seen how we can put the brakes on this behavior by synchronizing atomic variables.

Let's formalize a little more.

If operations are sequentially consistent, it means at the end of the day, when all is done and done, all the threads can kick their feet, open their behavior of choice, and all agree on the order in which memory changes occurred during the run. And that is the order specified by the code.

One won't say, "Didn't B happen before A? if the rest of them say, "A happened before B". They're all here,,

In particular, a thread, none of the acquires and releases can be reordered with one to another. This is in addition to the rules about what other memory accesses can be reordered around them.

This rule gives an additional level of sanity to the progression of atomic loads/acquires and stores/releases.

Every other operation in C involves a relaxation of the reordering rules, either for acquires/releases or other memory accesses, atomic or otherwise. You'd that if you really knew what you were doing and needed the speed boost. Here be armes of dragons...

More on that, but for now, let's stick to the safe and practical.

# 40.6 Atomic Assignments and Operators

Certain operators on atomic variables are atomic. And others aren't.

Let's start with a counter-example:

```
atomic_int x = 0;
```

```
thread1() {
 x = x + 3; // NOT atomic!
}
```

Since there's a read of x on the right side of the assignment and a write effectively on the left, these two operations. Another thread would sneak in the middle and make you unhappy.

But you can use the shorthand += to get an atomic operation:

```
atomic_int x = 0;
```

```
thread1() {
 x += 3; // ATOMIC!
}
```

In case, x will be atomically increased by 3—no another thread can jump in the middle.

In the following operations are atomic read-modify-write operations with sequential consistency, so use them with gleeful abandon. (In the example, a is atomic).

```
a++      a--      -a      ++a
a += b    a-= b    a *= b   a /= b   a%= b
a&= b    a|= b    a^= b   a>>= b   a<<= b
```

# 40.7 Library Functions that Automatically Synchronize

So far we've talked about how you can synchronize atomic variables, but it turns out there are a few library functions that do some behind-the-scenes synchronization, themselves.