
- **[Sutter04a]** H. Sutter. “Function Types” (*C/C++ Users Journal*, 22(7), July 2004).
- **[Sutter04b]** H. Sutter. “When and How to Use Exceptions” (*C/C++ Users Journal*, 22(8), August 2004).
- **[Sutter04c]** H. Sutter. “‘Just Enough’ Thread Safety” (*C/C++ Users Journal*, 22(9), September 2004).
- **[Sutter04d]** H. Sutter. “How to Provide (or Avoid) Points of Customization in Templates” (*C/C++ Users Journal*, 22(11), November 2004).
- **[SuttHysl01]** H. Sutter and J. Hyslop. “Hungarian wartHogs” (*C/C++ Users Journal*, 19(11), November 2001).
- **[SuttHysl02]** H. Sutter and J. Hyslop. “A Midsummer Night’s Madness” (*C/C++ Users Journal*, 20(8), August 2002).
- **[SuttHysl03]** H. Sutter and J. Hyslop. “Sharing Causes Contention” (*C/C++ Users Journal*, 21(4), April 2003).
- **[SuttHysl04a]** H. Sutter and J. Hyslop. “Getting Abstractions” (*C/C++ Users Journal*, 22(6), June 2004).
- **[SuttHysl04b]** H. Sutter and J. Hyslop. “Collecting Shared Objects” (*C/C++ Users Journal*, 22(8), August 2004).
- **[Taligent94]** *Taligent’s Guide to Designing Programs* (Addison-Wesley, 1994).
- **[Tsai01]** T. Tsai and N. Singh. “Libsafe 2.0: Detection of Format String Vulnerability Exploits” (Avaya Labs, March 2001).
- **[Vandevoorde03]** D. Vandevoorde and N. Josuttis. *C++ Templates* (Addison-Wesley, 2003).
- **[Webber03]** A. B. Webber. *Modern Programming Languages: A Practical Introduction* (Franklin, Beedle & Associates, 2003).

## Summary of Summaries

### Organizational and Policy Issues

- 0. Don’t sweat the small stuff. (Or: Know what not to standardize.)
  *Say only what needs saying: Don’t enforce personal tastes or obsolete practices.*

- 1. Compile cleanly at high warning levels.
  *Take warnings to heart: Use your compiler’s highest warning level. Require clean (warning-free) builds. Understand all warnings. Eliminate warnings by changing your code, not by reducing the warning level.*

- 2. Use an automated build system.
  *Push the (singular) button: Use a fully automatic (“one-action”) build system that builds the whole project without user intervention.*

- 3. Use a version control system.
  *The palest of ink is better than the best memory (Chinese proverb): Use a version control system (VCS). Never keep files checked out for long periods. Check in frequently after your updated unit tests pass. Ensure that checked-in code does not break the build.*

- 4. Invest in code reviews.
  *Re-view code: More eyes will help make more quality. Show your code, and read others’. You’ll all learn and benefit.*

### Design Style

- 5. Give one entity one cohesive responsibility.
  *Focus on one thing at a time: Prefer to give each entity (variable, class, function, namespace, module, library) one well-defined responsibility. As an entity grows, its scope of responsibility naturally increases, but its responsibility should not diverge.*

- 6. Correctness, simplicity, and clarity come first.
  *KISS (Keep It Simple Software): Correct is better than fast. Simple is better than complex. Clear is better than cute. Safe is better than insecure (see Items 83 and 99).*

- 7. Know when and how to code for scalability.
  *Beware of explosive data growth: Without optimizing prematurely, keep an eye on asymptotic complexity. Algorithms that work on user data should take a predictable, and preferably no worse than linear time complexity.*

- 8. Don't optimize prematurely.
  *Spur not a willing horse (Latin proverb): Premature optimization is as addictive as it is unproductive. The first rule of optimization is: Don't do it. The second rule of optimization (for experts only) is: Don't do it yet. Measure twice, optimize once.*

- 9. Don't pessimize prematurely.
  *Easy on yourself, easy on the code: All other things being equal, notably code complexity and readability, certain efficient design patterns and coding idioms should just flow naturally from your fingertips and are no harder to write than the pessimized alternatives. This is not premature optimization; it is avoiding gratuitous pessimization.*

- 10. Minimize global and shared data.
  *Sharing causes contention: Avoid shared data, especially global data. Shared data increases coupling, which reduces maintainability and often performance.*

- 11. Hide information.
  *Don't tell: Don't expose internal information from an entity that provides an abstraction.*

- 12. Know when and how to code for concurrency.
  *Thread safety: If your application uses multiple threads or processes, know how to minimize sharing objects where possible (see Item 10) and share the right ones safely.*

- 13. Ensure resources are owned by objects. Use explicit RAII and smart pointers.
  *Don't saw by hand when you have power tools: C++'s "resource acquisition is initialization" (RAII) idiom is the power tool for correct resource handling. RAII allows the compiler to provide strong and automated guarantees that in other languages require fragile hand-coded idioms. When allocating a raw resource, immediately pass it to an owning object. Never allocate more than one resource in a single statement.*

### Coding Style

- 14. Prefer compile- and link-time errors to run-time errors.
  *Don't put off 'til run time what you can do at build time: Prefer to write code that uses the compiler to check for invariants during compilation, instead of checking them at run time. Run-time checks are control- and data-dependent, which means you'll seldom know whether they are exhaustive. In contrast, compile-time checking is not control- or data-dependent and typically offers higher degrees of confidence.*

- 15. Use const proactively.
  *const is your friend: Immutable values are easier to understand, track, and reason about, so prefer constants over variables wherever it is sensible and make const your default choice when you define a value: It's safe, it's checked at compile time (see Item 14), and it's integrated with C++'s type system. Don't cast away const except to call a const-incorrect function (see Item 94).*

- **16. Avoid macros.**
  *TO PUT IT BLUNTLY: Macros are the bluntest instrument of C and C++'s abstraction facilities, ravenous wolves in functions' clothing, hard to tame, marching to their own beat all over your scopes. Avoid them.*

- **17. Avoid magic numbers.**
  *Programming isn't magic, so don't incant it: Avoid spelling literal constants like **42** or **3.14159** in code. They are not self-explanatory and complicate maintenance by adding a hard-to-detect form of duplication. Use symbolic names and expressions instead, such as **width * aspectRatio**.*

- **18. Declare variables as locally as possible.**
  *Avoid scope bloat, as with requirements so too with variables: Variables introduce state, and you should have to deal with as little state as possible, with lifetimes as short as possible. This is a specific case of Item 10 that deserves its own treatment.*

- **19. Always initialize variables.**
  *Start with a clean slate: Uninitialized variables are a common source of bugs in C and C++ programs. Avoid such bugs by being disciplined about cleaning memory before you use it; initialize variables upon definition.*

- **20. Avoid long functions. Avoid deep nesting.**
  *Short is better than long, flat is better than deep: Excessively long functions and nested code blocks are often caused by failing to give one function one cohesive responsibility (see Item 5), and both are usually solved by better refactoring.*

- **21. Avoid initialization dependencies across compilation units.**
  *Keep (initialization) order: Namespace-level objects in different compilation units should never depend on each other for initialization, because their initialization order is undefined. Doing otherwise causes headaches ranging from mysterious crashes when you make small changes in your project to severe non-portability even to new releases of the same compiler.*

- **22. Minimize definitional dependencies. Avoid cyclic dependencies.**
  *Don't be over-dependent: Don't **#include** a definition when a forward declaration will do.*

  *Don't be co-dependent: Cyclic dependencies occur when two modules depend directly or indirectly on one another. A module is a cohesive unit of release (see page 103); modules that are interdependent are not really individual modules, but super-glued together into what's really a larger module, a larger unit of release. Thus, cyclic dependencies work against modularity and are a bane of large projects. Avoid them.*

- **23. Make header files self-sufficient.**
  *Behave responsibly: Ensure that each header you write is compilable standalone, by having it include any headers its contents depend upon.*

- **24. Always write internal #include guards. Never write external #include guards.**
  *Wear head(er) protection: Prevent unintended multiple inclusions by using **#include** guards with unique names for all of your header files.*
