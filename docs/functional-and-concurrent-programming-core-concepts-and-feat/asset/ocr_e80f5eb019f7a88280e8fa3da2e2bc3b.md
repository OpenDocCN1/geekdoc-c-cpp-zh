# Chapter 18

# Atomicity and Locking

During the execution by a thread of a compound operation that consists of multiple steps, other threads can observe and interfere with the state of an application as it exists between these steps. By contrast, an atomic operation consists of a single step, with no possibility of disruption during that step. Locking is a mechanism that can be used to make a compound operation by a thread appear atomic to other threads, thereby preventing them from interfering during its execution in ways that would be detrimental to correctness. Different systems define their own locking mechanisms. In particular, Java defines a basic form of locks that can be used with any JVM language.

# 18.1 Atomicity

Chapter 17 discussed a program in which three threads shared a terminal to output the letters A, B, and C. The three letters could appear in different orders from run to run, and this nondeterminism was due to the unpredictable scheduling of threads.

Consider this variant in which, instead of sharing a terminal, two threads (in addition to main) share an integer value:¹

```
Scala
// DON'T DO THIS!
var shared = 0

def add(n: Int): Unit = n times (shared += 1)

val t1 = Thread(() => add(5), "T1")
val t2 = Thread(() => add(5), "T2")

t1.start(); t2.start()
t1.join(); t2.join()

println(shared)
```

Listing 18.1: Multiple threads share an integer unsafely.

¹Function times is used to repeat code n times. It was defined in Listing 12.4.