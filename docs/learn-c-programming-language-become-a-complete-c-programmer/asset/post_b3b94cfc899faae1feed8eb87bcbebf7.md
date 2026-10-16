
r2 = x.load(memory_order_relaxed);
y.store(42,memory_order_relaxed);

This is allowed to produce **r2==42**, making it appear that time went backward in thread 2. That is, **memory_order_relaxed** allows this execution order:

```
y.store(42,memory_order_relaxed);
r1 = y.load(memory_order_relaxed);
x.store(r1,memory_order_relaxed);
r2 = x.load(memory_order_relaxed);
```

For explanations, see the specialist literature, for example, [Boehm,2008] and [Williams,2012]. It is entirely architecture-specific whether a given memory order makes sense. Clearly, a relaxed memory model is not something to be directly used in applications programming. Utilizing a relaxed memory model is an even more specialized task than general lock-free programming. I see it as something done by a small subset of operating system kernel, device driver, and virtual machine implementers. It can also be useful in machine-generated code (as **gotos** can be). If two threads really do not directly share data, some machine architectures deliver significant performance improvements through the use of a relaxed memory model at the cost of complexity in the implementation of message-passing primitives (e.g., **future** and **promise**; §42.4.4). To allow significant optimizations for architectures with relaxed memory models, the standard provides an attribute **[[carries_dependency]]** for transmitting memory order dependencies across function calls (§iso.7.6.4). For example:

```
[[carries_dependency]] struct foo * f(int i)
{
// let the caller use memory_order_consume for the result:
return foo_head[i].load(memory_order_consume);
}
```

You can also put **[[carries_dependency]]** on function arguments, and there is a function **kill_dependency()** for stopping the propagation of such dependencies.

> One of the designers of the C++ memory model, Lawrence Crowl, summarizes:
>
> “Dependency ordering is probably the most complex concurrency feature. It’s really worth using when
> - you have a machine for which it matters,
> - you have a very high bandwidth read-mostly atomic data structure, and
> - you’re willing to spend a couple of weeks in testing and external reviews.
>
> This is real expert territory.”

Consider yourself warned.

```
// ...
int expected = val.load(); // read current value
do {
int next = fct(expected); // calculate new value
} while (!val.compare_exchange_weak(expected,next)); // write next to val or to expected
```

The atomic val.compare_exchange_weak(expected,next) reads the current value of val and compares it to expected; if equal, it writes next to val. If some other thread has written to val since we read it in preparation to an update, we have to try again. When we try again, we use the new value of expected obtained from compare_exchange_weak(). Eventually, the expected value will be written. The value of expected is “the current value of val as seen by this thread.” So, since expected is updated to the current value each time the compare_exchange_weak() is executed, we should never get an infinite loop.

Operations like compare_exchange_strong() are widely known as compare-and-swap operations (CAS operations). There is a potentially serious problem with all CAS operations (in any language and on any machine) known as the ABA problem. Consider adding a node at the head of a very simple lock-free singly-linked list if the data value is less than the head’s data:

```
extern atomic<Link*> head; // the shared head of a linked list
Link * nh = new Link(data,nullptr); // make a link ready for insertion
Link*h = head.load(); // read the shared head of the list
do {
if (h->data<data) break; // if so, insert elsewhere
nh->next = h; // next element is the previous head
} while (!head.compare_exchange_weak(h,nh)); // write nh to head or to h
```

This is a simplified version of code that would insert data at the right position in an ordered linked list. I read the head, use it as the next of my new Link, and then write the pointer to my new Link to head. I do that repeatedly until no other thread has managed to change the head while I was getting nh ready.

Let us examine this code in some detail. Call the value of head that I read A. If no other thread changed the value of head before I executed my compare_exchange_weak(), it finds A in head and succeeds in replacing it with my nh. If some other thread changed the value of head to B after I read A, my compare_exchange_weak() will fail, and I’ll go around my loop to read head again.

This looks right. What could possibly go wrong? Well, after I read the value A, some other thread changed the value of head to B and recycled the Link. Then, some thread reused the node A and reinserted it at the head of the list. Now my compare_exchange_weak() finds A and does the update. However, the list had changed; the value of head went from A to B and then back to A. That change may be significant in many different ways, but in this simplified example, A->data may have changed so that the critical data comparison may be wrong. ABA problems can be very subtle and hard to detect. There are a variety of ways of dealing with the ABA problem [Dechev,2010]. I mention it here primarily to warn about the subtleties of lock-free programming.

prevents that. The `!x_init` relies on the implicit conversion from an `atomic<T>` to a `T`. This code can be simplified further by using RAII (§42.3.1.4).

The double-checked locking idiom is represented in the standard library by `once_flag` and `call_once()` (§42.3.3), so you don’t have to write such code directly.

The standard library also supports atomic pointers:

## `atomic<T>` for Pointers (§iso.29.6.4)

- `x.val` represents the value of the atomic `x`; all operations are `noexcept`
- `z=x.fetch_add(y) x.val+=y`; `z` is the previous `x.val`
- `z=x.fetch_add(y,order) z=x.fetch_add(y)`; use `order`
- `z=x.fetch_sub(y) x.val-=y`; `z` is the previous `x.val`
- `z=x.fetch_sub(y,order) z=x.fetch_sub(y)`; use `order`
- `++x ++x.val`; return `x.val`
- `x++ x.val++;` return previous `x.val`
- `--x --x.val`; return `x.val`
- `x-- x.val--;` return previous `x.val`
- `x+=y x.val+=y`; return `x.val`
- `x-=y x.val-=y`; return `x.val`

To allow the C standard library to be compatible, the `atomic` member function types have freestanding equivalents:

## `atomic_*` operations (§iso.29.6.5) (continues) All operations are `noexcept`

- `atomic_is_lock_free(p)`
- `atomic_init(p,v)`

Are objects of `*p`’s type atomic? Initialize `*p` with `v`

- `atomic_store(p,v)` Store `v` in `*p`
- `x=atomic_load(p)` Load `*p` into `x`
- `atomic_*` operations (continued) (§iso.29.6.5)
- All operations are `noexcept`
- Store `v` in `*p`
- Assign `*p` to `x`. Load `*p` into `x`
- `b=atomic_compare_exchange_weak(p,q,v)` Compare and exchange `*p` and `*q`; `b=(*q==v)` … about 70 more functions …

## 41.3.2 Flags and Fences

In addition to the support for atomic types, the standard library offers two lower-level synchronization facilities: atomic flags and fences. The primary use of these is to implement the lowest-level atomic facilities, such as spinlocks and the atomic types. They are the only lock-free mechanisms that are guaranteed to be supported on every implementation (though all major platforms support atomic types).

Essentially no programmers need to use flags or fences. Those who do usually work closely with machine architects.

### 41.3.2.1 atomic Flags

An atomic_flag is the simplest atomic type and the only one with operations guaranteed to be atomic for every implementation. An atomic_flag represents a single bit of information. If necessary, the other atomic types can be implemented using atomic_flag.

The two possible values of an atomic_flag are called set and clear.

## atomic_flag (§iso.29.7)

All operations are noexcept

atomic_flag fl; The value of fl is undefined
atomic_flag fl {}; Default construct: the value of fl is 0
atomic_flag fl {ATOMIC_FLAG_INIT}; Initialize fl to clear
b=fl.test_and_set() Set fl and b is fl’s old value
b=fl.test_and_set(order) Set fl and b is fl’s old value; use memory order order
fl.clear() Clear fl
fl.clear(order) Clear fl; use memory order order
b=atomic_flag_test_and_set(flp) Set *flp; b is *flp’s old value
b=atomic_flag_test_and_set_explicit(flp,order) Set *flp; b is *flp’s old value; use memory order order
atomic_flag_clear(flp) Clear *flp
atomic_flag_clear_explicit(flp,order) Clear *flp; use memory order order

The bool return values are true for set and false for clear.

Using {} to initialize atomic_flag seems to make sense. However, there is no guarantee that 0 represents clear. A machine where clear is 1 is rumored to exist. Clearing using ATOMIC_FLAG_INIT is the only portable and reliable way of initializing an atomic_flag. The ATOMIC_FLAG_INIT is an implementation-supplied macro.

You can think of an atomic_flag as a very simple spin lock:

```
class spin_mutex {
atomic_flag flag = ATOMIC_FLAG_INIT;
public:
void lock() { while(flag.test_and_set()); }
void unlock() { flag.clear(); }
};
```

Note that spin locks can easily become very expensive.

As usual, I leave the memory orders and their proper use to the specialist literature.

### 41.3.2.2 Fences

A fence, also known as a memory barrier, is an operation that restricts operation reordering according to some specified memory ordering (§41.2.3). The fence operations do not do anything else. Think of them as simply slowing down a program to a safe speed, allowing the memory hierarchy to reach a reasonably well-defined state.

atomic_thread_fence(order)
atomic_signal_fence(order)

## Fences (§iso.29.8)

All operations are noexcept

Enforce memory order order
Enforce memory order order
