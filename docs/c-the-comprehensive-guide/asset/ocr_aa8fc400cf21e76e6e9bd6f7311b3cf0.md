There are (especially since C++20) rules about what you should not do with a `volatile` variable:

+   - Do not use it as a synchronization mechanism between threads. There are other mechanisms that are better and safer for this purpose.
+   - Do not use compound assignments like `x += 1` or `v |= 0x03` on a volatile variable. It may—but does not have to—result in two accesses to the variable, which would be inconsistent. However, you may write `x = x + 1` or `v = v | 0x03` as it is clear that there is one read and one write operation. Also, `++x` is allowed.