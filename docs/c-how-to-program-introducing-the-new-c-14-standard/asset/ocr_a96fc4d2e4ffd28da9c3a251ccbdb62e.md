# 4.14 Fundamental Types Are Not Portable

The table in **Appendix C** lists C++’s fundamental types. Like its predecessor language C, C++ requires all variables to have a type. In C and C++, programmers frequently have to write separate versions of programs to support different computer platforms, because the fundamental types are not guaranteed to be identical from computer to computer. For example, an `int` on one machine might be represented by 16 bits (2 bytes) of memory, on a second machine by 32 bits (4 bytes), and on another machine by 64 bits (8 bytes).

![](bbox=[0.12, 0.55, 0.194, 0.608])

# Portability Tip 4.2

*C++’s fundamental types are not portable across all computer platforms that support C++.*