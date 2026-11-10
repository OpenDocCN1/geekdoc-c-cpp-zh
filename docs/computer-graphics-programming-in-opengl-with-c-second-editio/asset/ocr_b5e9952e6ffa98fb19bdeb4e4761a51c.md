phases don’t require the generation of additional rays (collision detection, lighting/shadows, and texturing). However, the reflection and refraction phases both require generating a new ray and running `process_stack_element()` on the new ray(s). Since there is no way in GLSL to make such a call recursively, we adjust the contents of the current stack element to keep track of where we left off, push a new stack element containing the new ray to be processed, and then exit `process_stack_element()`. The driver function — the new version of `rayTrace()` — then continues iteratively calling `process_stack_element()` until every stack element (every ray) has had a chance to complete all five phases. The end result is the same as if recursion had been available.

The code in Program 16.12 (the declarations, and the `push()`, `pop()`, `process_stack_element()`, and `rayTrace()` functions) replaces the previous `rayTrace()` function (and its “children” `rayTrace2()` and `rayTrace3()`) from Program 16.11. The remainder of Program 16.12 is unchanged from Program 16.11.

The output of Program 16.12 depends on the `max_depth` setting. The larger the value, the longer the sequence of rays that can be generated. Figure 16.19 shows the outputs for `max_depth` values of 0, 1, 2, 3, and 4.

![](bbox=[0.21, 0.54, 0.79, 0.86])

**Figure 16.19**
Output of Program 16.12, showing recursive depth values of 0, 1, 2, 3, and 4 (left-to-right, top-to-bottom)