+   - lazily computed sequences (known as generators; Section 18.4) that produce one value at a time on demand;⁴
+   - event-driven coding without callback functions⁵—for example, simulations, user interfaces, servers, games, non-blocking I/O;⁶
+   - cooperative multitasking;⁷˒⁸
+   - structured concurrency;⁹
+   - reactive streams programming;¹⁰ and
+   - implementing state machines.¹¹

# 18.2 Coroutine Support Libraries

Coroutines require various supporting classes with numerous member functions and nested types. Creating these yourself is cumbersome, complex and error-prone. The C++20 standard library includes only the low-level primitives that library writers need to build coroutines support libraries. Lewis Baker, who has worked on several such libraries, said that these primitives “can be thought of as a low-level assembly language for coroutines.”¹² Most developers will prefer to work with a coroutine support library. Standard library coroutine support is expected in C++23.¹³˒¹⁴

In the interim, the open-source community has created several non-standard experimental coroutine support libraries. Here are the ones we considered for this presentation:

+   4. “Coroutines,” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/language/coroutines.
+   5. David Mazières, “My Tutorial and Take on C++20 Coroutines,” February 2021. Accessed April 18, 2023. https://www.scs.stanford.edu/~dm/blog/c++-coroutines.html.
+   6. Techmunching, “Coroutines and Their Introduction in C++, May 30, 2020. Accessed April 18, 2023. https://techmunching.com/coroutines-and-their-introduction-in-c/.
+   7. Rainer Grimm, “C++20: More Details to Coroutines,” March 27, 2020. Accessed April 18, 2023. http://modernescpp.com/index.php/component/content/article/54-blog/c-20/488-c-20-coroutines-more-details.
+   8. Bobby Priambodo, Cooperative vs. Preemptive: A Quest to Maximize Concurrency Power, September 3, 2019. Accessed April 18, 2023. https://medium.com/traveloka-engineering/cooperative-vs-preemptive-to-maximize-concurrency-power-3b10c5a920fe.
+   9. Lewis Baker, “Structured Concurrency: Writing Safer Concurrent Code with Coroutines and Algorithms,” October 14, 2019. Accessed April 18, 2023. https://www.youtube.com/watch?v=IwYySq3s2rg.
+   10. Jeff Thomas, “Exploring Coroutines,” April 7, 2021. Accessed April 18, 2023. https://blog.coffeecode.com/2021/04/exploring-coroutines/.
+   11. Steve Downey, “Converting a State Machine to a C++20 Coroutine,” June 29, 2021. Accessed April 18, 2023. https://www.youtube.com/watch?v=Z8jHi9Cs6Ug.
+   12. Lewis Baker, “C++ Coroutines: Understanding Operator co_await,” November 17, 2017. Accessed April 18, 2023. https://lewissbaker.github.io/2017/11/17/understanding-operator-co-await.
+   13. Ville Voutilainen, “To Boldly Suggest an Overall Plan for C++23,” November 25, 2019. Accessed April 18, 2023. http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p0529r4.html.
+   14. “C++23.” Accessed April 18, 2023. https://en.wikipedia.org/wiki/C%2B%2B23.