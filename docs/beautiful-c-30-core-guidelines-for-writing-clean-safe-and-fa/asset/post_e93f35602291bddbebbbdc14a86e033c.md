
No, it is not. The right thing to do is to add a constructor that performs this initialization, like so:

```cpp
struct Agg {
    Agg() : a{0}, b{0}, c{0} {};
    int a;
    int b;
    int c;
};
```

“But now it’s not an aggregate anymore,” you observe, correctly. “I want that brace initialization feature and memset, please.”

All right then, what you can do is use member initializers, like this:

```cpp
struct Agg {
    int a = 0;
    int b = 0;
    int c = 0;
};
```

Now if you declare

```cpp
auto t = Agg{};
```

t.a will be initialized with = 0, as will t.b and t.c. Even better, you can use designated initializers, new to C++20, which allow parts of the object to be initialized with different values, like this:

```cpp
auto t = Agg{.c = 21};
```

Now, t.a and t.b will still be initialized with 0, but t.c will be initialized with 21.

“All right, yes, designated initializers are nice and it’s back to being an aggregate,” (I can sense a “but” forming in your consciousness) “but the members are still being initialized one at a time! I want to use memset to initialize them in a single instruction.”

That is a really bad idea. You are separating the initialization of the object from its definition. What happens when you add members to the aggregate? Your call to memset will only cover part of the object. C++ allows you to collect the whole life cycle of an object into a single abstraction, the class, which is of immense value. You should not try and subvert it.

“I shall use sizeof to ensure that I remain independent of any changes to the class.”

Still not a good idea. What if you introduce a member that does NOT default to zero initialization? You will then have to ensure that your memset call honors the value of that member, perhaps by splitting it into two. That is simply an accident waiting to happen.

“I do not accept this! I own the aggregate, it is defined in a private implementation file, not a header, it is NOT going to be modified in nature without my knowledge, it is TOTALLY SAFE to call memset! What is going on here? Why shouldn’t I call memset?”

Well, the fact of the matter is that you do not actually need to call memset. Let’s talk about the abstract machine.

## What is the standard talking about anyway?

P.2: “Write in ISO Standard C++” is one of the first Core Guidelines. The standard dictates how a conforming implementation of C++ behaves. Any divergence from this is not standard C++. There are many implementations of C++ for many platforms, all of which behave in different ways depending on things like the machine word size and other target-specific features. Some platforms do not feature offline storage in the form of disk drives. Others do not feature a standard input. How does the standard accommodate all this variation?

The first three clauses of the standard are Scope,³ Normative references,⁴ and Terms and definitions.⁵ On pages 10 to 12, the fourth clause, General principles,⁶ precisely explains this problem. This is only one of the reasons why it is important to RTFM (Read The Front Matter).

- 3. https://eel.is/c++draft/intro.scope
- 4. https://eel.is/c++draft/intro.refs
- 5. https://eel.is/c++draft/intro.defs
- 6. https://eel.is/c++draft/intro

The first four clauses that make up the front matter tell you how the document is structured, what the conventions are, what “undefined behavior” means, what an “ill-formed program” is: in fact, the entire frame of reference is described here. In the General principles clause, in particular in section [intro.abstract],⁷ you will find the following text:

- 7. https://eel.is/c++draft/intro.abstract

> “The semantic descriptions in this document define a parameterized nondeterministic abstract machine. This document places no requirement on the structure of conforming implementations. In particular, they need not copy or emulate the structure of the abstract machine. Rather, conforming implementations are required to emulate (only) the observable behavior of the abstract machine as explained below.”

A footnote is attached to this paragraph, which says:

> “This provision is sometimes called the “as-if” rule, because an implementation is free to disregard any requirement of this document as long as the result is as if the requirement had been obeyed, as far as can be determined from the observable behavior of the program. For instance, an actual implementation need not evaluate part of an expression if it can deduce that its value is not used and that no side effects affecting the observable behavior of the program are produced.”

This is a marvelous get-out clause (more correctly, get-out paragraph). All that an implementation must do is emulate the observable behavior. This means it can look at your code, examine the result of its execution, and do whatever is necessary to match that result. This is how optimization works: by looking at a result and substituting the optimal set of instructions required for achieving it.

What does this mean for our example aggregate class?

Since the member initializers are all zero, the compiler will see that a default instantiation of an Agg object will set three ints to zero. This is identical to a call to memset, so it will probably call memset. A manual call to memset is unnecessary.

But wait! The class consists of only three integers. On a typical 64-bit platform with 32-bit integers, this means that only 12 bytes need to be set to zero. This can be done in two instructions on an x64 platform. Why on earth would you want to call memset? We can check this by visiting the Compiler Explorer website and trying out some code:

```cpp
struct Agg {
    int a = 0;
    int b = 0;
    int c = 0;
};
void fn(Agg&);

int main() {
    auto t = Agg{}; // (1)
    fn(t);          // (2)
}
```

The function call at (2) prevents the compiler from optimizing away t.

The x86-64 gcc compiler, with the optimization flag set to -O3, yields the following:

```asm
main:
    sub rsp, 24
    mov rdi, rsp
    mov QWORD PTR [rsp], 0   // (1)
    mov DWORD PTR [rsp+8], 0
    call fn(Agg&)            // (2)
    xor eax, eax
    add    rsp, 24
    ret
```

We can see the two mov instructions doing the work of zeroing the three ints. The compiler writer knows that this is the fastest way of setting three ints to zero. If there were many more members to be set to zero, the MMX instruction set would be brought into play. The joy of the Compiler Explorer website is that you can try this out yourself very easily.

We hope this convinces you not to use memset.

## But what about memcpy?

Just as I would use memset in my C programs to zero a struct, so would I use memcpy to assign it to another instance. C++ assignment is very similar to initialization: by default, it copies data member-wise in the order of declaration using the assignment operator of that member’s type. You can write your own assignment operator, and, unlike the constructor, it does not start by implicitly performing a member-wise copy. You might think the argument for calling memcpy is stronger here, but for the same reasons as above, it is neither a good idea nor necessary. We can return to the Compiler Explorer website and make a modest change to the source:

```cpp
struct Agg {
    int a = 0;
    int b = 0;
    int c = 0;
};

void fn(Agg&);

int main() {
    auto t = Agg{}; // (1)
    fn(t);        // (2)
    auto u = Agg{}; // (3)
    fn(u);        // (4)
    t = u;        // (5)
    fn(t);        // (6)
}
```

This now yields the following:

```asm
main:
    sub     rsp, 40
    mov     rdi, rsp
    mov     QWORD PTR [rsp], 0          // (1)
    mov     DWORD PTR [rsp+8], 0
    call    fn(Agg&)                    // (2)
    lea     rdi, [rsp+16]
    mov     QWORD PTR [rsp+16], 0       // (3)
    mov     DWORD PTR [rsp+24], 0
    call    fn(Agg&)                    // (4)
    mov     rax, QWORD PTR [rsp+16]     // (5)
    mov     rdi, rsp                    // (6)
    mov     QWORD PTR [rsp], rax        // (5)
    mov     eax, DWORD PTR [rsp+24]
    mov     DWORD PTR [rsp+8], eax
    call    fn(Agg&)                    // (6)
    xor     eax, eax
    add     rsp, 40
    ret
```

As you can see, the compiler has generated the same QWORD/DWORD trick and has emitted code to directly copy the memory from the original object in four instructions. Again, why would you call memcpy?
