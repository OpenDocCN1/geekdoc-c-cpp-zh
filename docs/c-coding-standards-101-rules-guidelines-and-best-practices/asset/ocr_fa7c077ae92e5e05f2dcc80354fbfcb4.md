+   8. Don't optimize prematurely.
+      Spur not a willing horse (Latin proverb): Premature optimization is as addictive as it is unproductive. The first rule of optimization is: Don't do it. The second rule of optimization (for experts only) is: Don't do it yet. Measure twice, optimize once.

+   9. Don't pessimize prematurely.
+      Easy on yourself, easy on the code: All other things being equal, notably code complexity and readability, certain efficient design patterns and coding idioms should just flow naturally from your fingertips and are no harder to write than the pessimized alternatives. This is not premature optimization; it is avoiding gratuitous pessimization.

+   10. Minimize global and shared data.
+       Sharing causes contention: Avoid shared data, especially global data. Shared data increases coupling, which reduces maintainability and often performance.

+   11. Hide information.
+       Don't tell: Don't expose internal information from an entity that provides an abstraction.

+   12. Know when and how to code for concurrency.
+       Thread safety: If your application uses multiple threads or processes, know how to minimize sharing objects where possible (see Item 10) and share the right ones safely.

+   13. Ensure resources are owned by objects. Use explicit RAII and smart pointers.
+       Don't saw by hand when you have power tools: C++'s "resource acquisition is initialization" (RAII) idiom is the power tool for correct resource handling. RAII allows the compiler to provide strong and automated guarantees that in other languages require fragile hand-coded idioms. When allocating a raw resource, immediately pass it to an owning object. Never allocate more than one resource in a single statement.

# ## Coding Style

+   14. Prefer compile- and link-time errors to run-time errors.
+       Don't put off 'til run time what you can do at build time: Prefer to write code that uses the compiler to check for invariants during compilation, instead of checking them at run time. Run-time checks are control- and data-dependent, which means you'll seldom know whether they are exhaustive. In contrast, compile-time checking is not control- or data-dependent and typically offers higher degrees of confidence.

+   15. Use const proactively.
+       const is your friend: Immutable values are easier to understand, track, and reason about, so prefer constants over variables wherever it is sensible and make const your default choice when you define a value: It's safe, it's checked at compile time (see Item 14), and it's integrated with C++'s type system. Don't cast away const except to call a const-incorrect function (see Item 94).