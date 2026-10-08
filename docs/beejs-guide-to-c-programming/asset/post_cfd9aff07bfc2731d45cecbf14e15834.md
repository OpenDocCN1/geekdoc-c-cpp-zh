
```cpp
};

_Atomic(struct point) p;

printf("Is lock free: %d\n", atomic_is_lock_free(&p));
}
```

Here's the catch: you can't access fields of an atomic struct or union... so what's the point? Well, you can atomically copy the entire struct into a non-atomic variable and then use it. You can atomically copy the other way, too.

```cpp
#include <stdio.h>
#include <stdatomic.h>

int main(void)
{
    struct point {
        float x, y;
    };

    _Atomic(struct point) p;
    struct point t;

    p = (struct point){1, 2}; // Atomic copy

    printf("%f\n", p.x); // Error
    t = p; // Atomic copy

    printf("%f\n", t.x); // OK!
}
```

You can declare a struct where individual fields are atomic. It is implementation defined if atomic types are allowed on fields.

## 40.12 Atomic Pointers

Just a note here about placement of Atomic when it comes to pointers.

First, pointers to atomics (i.e. the pointer value is not atomic, but the thing it points to is):

```cpp
_Atomic int x;
_Atomic int *p; // p is a pointer to an atomic int
```

Second, atomic pointers to non-atomic values (i.e. the pointer value itself is atomic, but the thing it points to is not):

```cpp
int x;
int *_Atomic p; // p is an atomic pointer to an int
```

```cpp
p = &x; // OK!
```

Lastly, atomic pointers to atomic values (i.e. the pointer and the thing it points to are both atomic):

```cpp
_Atomic int x;
_Atomic *_Atomic p; // p is an atomic pointer to an atomic int
```

## 40.13 Memory Order

p = &x; // OK!

We've already talked about sequential consistency, which is the sensible one of the bunch. But there are a number of other ones:

| memory_order | Description |
| --- | --- |
| memory_order_seq_cst | Sequential Consistency |
| memory_order_acq_rel | Acquire/Release |
| memory_order_release | Release |
| memory_order_acquire | Acquire |
| memory_order_consume | Consume |
| memory_order_relaxed | Relaxed |

You can specify others with certain library functions. For example, you can add a value to an atomic variable like this:

```cpp
atomic_int x = 0;
x += 5; // Sequential consistency, the default
```

Or you can do the same with this library function:

```cpp
atomic_int x = 0;
atomic_fetch_add(&x, 5); // Sequential consistency, the default
```

Or you can do the same thing with an explicit memory ordering:

```cpp
atomic_int x = 0;
atomic_fetch_add_explicit(&x, 5, memory_order_seq_cst);
```

But what if we didn't want sequential consistency? And you wanted acquire/release instead for whatever reason? Just name it:

```cpp
atomic_int x = 0;
```

```cpp
atomic_fetch_add_explicit(&x, 5, memory_order_acq_rel);
```

We'll do a breakdown of the different memory orders, below. Don't mess with anything other than sequential consistency unless you know what you're doing. It's really easy to make mistakes that will cause quite, hard-to-reproduce fails.

### 40.1.3 Sequential Consistency

- Load operations acquire (see below).
- Store operations release (see below).
- Read-modify-write operations acquire then release.

Also, in order to maintain the total order of acquires and releases, no acquires or releases will be reordered with respect to each other. (The acquire/release rules do not forbid reordering a release followed by an acquire. But the sequentially consistent rules do.)

## Chapter 40. Atoms

### 40.13.2 Acquire

This is what happens on a load/read operation on an atomic variable.

- If another thread released this atomic variable, all the writes that thread did are now visible in this thread.
- Memory accesses in this thread that happen after this load can't be reordered before it.

### 40.13.3 Release

This is what happens on a store/write of an atomic variable.

- If another thread acquires this atomic variable, all memory writes in this thread before atomic write become visible to that other thread.
- Memory accesses in this thread that happen before the release can't be reordered after it.

### 40.13.4 Consume

This is an old one, similar to a less-strict version of acquire. It affects memory accesses that are data-dependent on the atomic variable.

Being “data dependent” vaguely means that the atomic variable is used in a calculation.

That is, if a thread consumes an atomic variable then all operations in that thread that go on to use that atomic variable will be able to see the memory writes in the releasing thread.

Compare with acquire memory writes in the releasing will will be visible to all operations in the current thread, not just the data-dependent ones.
Also acquire, there is a restriction on what operations can be reordered before consume. With acquire, you couldn't reorder anything before it. With consume, you can't reorder anything that depends on the loaded atomic value before.

### 40.13.5 Acquire/Release

This only applies to read-modify-write operations. It's an acquire and release bundled into one.

- An acquire happens for the read.
- A release happens for the write.

### 40.13.6 Relaxed

No rules; it's anarchy! Everyone can reorder everything! Dogs and cats living together—mass hysteria!
Actually, there is a rule. Atomic reads and writes are all-or-nothing. The operations can be reordered whimsically and there is zero synchronization between threads.

There are a few cases for this memory order, which you can find with a tiny bit of searching, e.g. simple counters.

And you can use a fence to force synchronization after a bunch of relaxed writes.

## 40.14 Fences

You know the releases and acquires of atomic variables occur as you read and write them?

Well, it’s possible to do a release or acquire without an atomic variable, as well.

## Chapter 40. Atoms

### 296

This is called a fence. So if you want all the effects of non-atomic operations to be visible elsewhere, you can put up a release in one thread and an acquire in another, like how atomic operations work.

You can put up a fence with any specified order:

```cpp
atomic_thread_fence(memory_order_acquire);
```

There's also a lighter version of the fence for use with signal handlers, called atomic_signal_fence().

It works the same way as atomic_thread_fence(), except:

- It only deals with visibility within the same thread; no hardware instructions are emitted.

If you want to be sure atomic operations are visible in the signal handler, you can use this fence.

Because consume is all the operations that are dependent on the value of the acquired variable, and there is no variable with it. The idea is that the signal handler is executing in this thread, not another, so this haven't been reordered.

## 40.15 References

If you want to learn more about this stuff, here are some of the things that helped me plow through:

- Herb Sutter's Weapons:
  - Part 1
  - Part 2

- Jeff Preston's materials, in particular:
  - An Introduction to Lock-Free Programming
  - Acquire and Release Semantics
  - The Happens-After Relation
  - The Synchronizes-With Relation
  - The Purpose of memory_order_consume in C++
  - You Can Do Any Atomic Read-Write Operation

- CPPReference:
  - Memory Order
  - Atomic Types

- Bruce Dawn's Lockless Programming Considerations

Because consume is all the operations that are dependent on the value of the acquired variable, and there is no variable with it.
