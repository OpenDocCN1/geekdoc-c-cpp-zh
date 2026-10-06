# ISO/IEC 14882:2017(E)

```
id() noexcept;
4   Effects: Constructs an object of type id.
5   Postconditions: The constructed object does not represent a thread of execution.
6   bool operator=(thread::id x, thread::id y) noexcept;
7   Returns: true only if x and y represent the same thread of execution or neither x nor y represents a
      thread of execution.
   bool operator!=(thread::id x, thread::id y) noexcept;
8   Returns: (x != y)
   bool operator<(thread::id x, thread::id y) noexcept;
9   Returns: A value which operator< is a total ordering as described in 27.8.
   bool operator>(thread::id x, thread::id y) noexcept;
10  Returns: (y < x).
   bool operator<=(thread::id x, thread::id y) noexcept;
11  Returns: (x <= y).
   template<class charT, class traits>
   basic_ostream<charT, traits>&
   operator=(basic_ostream<charT, traits>& out, thread::id id);
12  Effects: Inserts an unspecified text representation of id into. For two objects of type thread::id
      x and y, if x == y the id objects have the same text representation and if x != y the
      thread::id objects shall have distinct text representations.
13  Returns:
   template < struct hash<thread::id>;
14  The specialization is enabled (23.14.15).
```

# 33.3.2.2 thread constructors

```
thread() noexcept;
1   Effects: Constructs a thread that does not represent a thread of execution.
2   Postconditions: get_id() == id().n   template<class F, class... Args>
3   Requires: F and each Ti in Args shall satisfy the MoveConstructible requirements. INVOKE(DECA-
      COPY(std::forward<F>(f)), DECA_COPY(std::forward<Args>(args))...) (23.14.3) shall be a va-
      lid expression.
4   Remarks: This constructor shall not participate in overload resolution if decay_t<F> is the same type
      as std::thread.
5   Effects: Constructs an object of type thread. The new thread of execution executes INVOKE(
      DECA_COPY(std::forward<F>(f)), DECA_COPY(std::forward<Args>(args))...) with the calls
      to DECA_COPY being evaluated in constructing the thread. Any return value from this invocation
```

§ 33.3.2.2                               ©ISO/IEC 2017 - All rights reserved                               1360