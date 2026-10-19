```
unsigned char d = c;    // OK, d has an indeterminate value
int e = d;              // undefined behavior
return b ? d : 0;       // undefined behavior if b is true
}
```

— end example]

# 6.7.5 Storage duration [basic.stc]

# 6.7.5.1 General [basic.stc.general]

1 The storage duration is the property of an object that defines the minimum potential lifetime of the storage containing the object. The storage duration is determined by the construct used to create the object and is one of the following:

+   (1.1) — static storage duration
+   (1.2) — thread storage duration
+   (1.3) — automatic storage duration
+   (1.4) — dynamic storage duration

2 Static, thread, and automatic storage durations are associated with objects introduced by declarations (6.2) and implicitly created by the implementation (6.7.7). The dynamic storage duration is associated with objects created by a new-expression (7.6.2.8).

3 The storage duration categories apply to references as well.

4 When the end of the duration of a region of storage is reached, the values of all pointers representing the address of any part of that region of storage become invalid pointer values (6.8.3). Indirection through an invalid pointer value and passing an invalid pointer value to a deallocation function have undefined behavior. Any other use of an invalid pointer value has implementation-defined behavior.35

# 6.7.5.2 Static storage duration [basic.stc.static]

1 All variables which do not have dynamic storage duration, do not have thread storage duration, and are not local have static storage duration. The storage for these entities lasts for the duration of the program (6.9.3.2, 6.9.3.4).

2 If a variable with static storage duration has initialization or a destructor with side effects, it shall not be eliminated even if it appears to be unused, except that a class object or its copy/move may be eliminated as specified in 11.10.6.

3 The keyword static can be used to declare a local variable with static storage duration.
[Note 1: 8.8 describes the initialization of local static variables; 6.9.3.4 describes the destruction of local static variables. — end note]

4 The keyword static applied to a class data member in a class definition gives the data member static storage duration.

# 6.7.5.3 Thread storage duration [basic.stc.thread]

1 All variables declared with the thread_local keyword have thread storage duration. The storage for these entities lasts for the duration of the thread in which they are created. There is a distinct object or reference per thread, and use of the declared name refers to the entity associated with the current thread.

2 [Note 1: A variable with thread storage duration is initialized as specified in 6.9.3.2, 6.9.3.3, and 8.8 and, if constructed, is destroyed on thread exit (6.9.3.4). — end note]

# 6.7.5.4 Automatic storage duration [basic.stc.auto]

1 Block-scope variables not explicitly declared static, thread_local, or extern have automatic storage duration. The storage for these entities lasts until the block in which they are created exits.

2 [Note 1: These variables are initialized and destroyed as described in 8.8. — end note]

3 If a variable with automatic storage duration has initialization or a destructor with side effects, an implementation shall not destroy it before the end of its block nor eliminate it as an optimization, even if it appears to be unused, except that a class object or its copy/move may be eliminated as specified in 11.10.6.