# Section 17.8 Processing `new` Failures

+   - The C++ standard document specifies that, when operator `new` fails, it throws a `bad_alloc` exception (p. 769), which is defined in header `<new>`.
+   - Function `set_new_handler` (p. 769) takes as its argument a pointer to a function that takes no arguments and returns `void`. This pointer points to the function that will be called if `new` fails.
+   - Once `set_new_handler` registers a `new` handler (p. 771) in the program, operator `new` does not throw `bad_alloc` on failure; rather, it defers the error handling to the `new`-handler function.
+   - If `new` allocates memory successfully, it returns a pointer to that memory.