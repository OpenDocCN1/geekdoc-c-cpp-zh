# # 13.11 Volatile with “volatile”

The const and volatile keywords are often mentioned together. There are two reasons for this: first, they form the common group of cv-qualifiers in the standard; and second, volatile is somewhat the opposite of const. With volatile, you mark things that can be changed particularly easily. This refers to the control of the compiler: with volatile, you mark those variables and fields that can change at any time from the perspective of the processor and compiler without their intervention—through some other external mechanisms.

# ## C++20: Fewer “volatile”

In C++20, volatile was significantly pruned. “dubious and defective parts” were removed, while the “useful ones remained,” as J. F. Bastien stated in a lecture. [21]

Historically, volatile can appear anywhere const appear. This is nonsensical and confuses both programmers and compiler builders alike. Just because a parameter can be const, this was also allowed for volatile, which is quite pointless or at least confusing:

```
int func(volatile int x); // volatile is pointless here
```