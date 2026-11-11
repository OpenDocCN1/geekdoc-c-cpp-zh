+   9. What are the two steps in locating a nonlocal variable in a static-scoped
+   language with stack-dynamic local variables and nested subprograms?
+   10. Define static chain, static_depth, nesting_depth, and chain_offset.
+   11. What is an EP, and what is its purpose?
+   12. How are references to variables represented in the static-chain method?
+   13. Name three widely used programming languages that do not allow
+   nested subprograms.
+   14. What are the two potential problems with the static-chain method?
+   15. Explain the two methods of implementing blocks.
+   16. Describe the deep-access method of implementing dynamic scoping.
+   17. Describe the shallow-access method of implementing dynamic scoping.
+   18. What are the two differences between the deep-access method for nonlocal
+   access in dynamic-scoped languages and the static-chain method
+   for static-scoped languages?
+   19. Compare the efficiency of the deep-access method to that of the shallow-
+   access method, in terms of both calls and nonlocal accesses.

# PROBLEM SET

+   1. Show the stack with all activation record instances, including static and
+   dynamic chains, when execution reaches position 1 in the following skel-
+   etal program. Assume bigsub is at level 1.

```
```
function bigsub() {
    function a() {
        function b() {
            ... <---------------------- 1
        } // end of b
        function c() {
            ...
            b();
            ...
        } // end of c
        ...
        c();
        ...
    } // end of a
    ...
    a();
    ...
} // end of bigsub
```
```