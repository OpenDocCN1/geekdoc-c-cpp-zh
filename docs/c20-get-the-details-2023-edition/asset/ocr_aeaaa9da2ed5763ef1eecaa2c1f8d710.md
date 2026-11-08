```
```cpp
1 template <typename T>
2 auto add(T first, T second) {
3     return first + second;
4 }
5
6 #ifdef INSIGHTS_USE_TEMPLATE
7 template<>
8 int add<bool>(bool first, bool second)
9 {
10     return static_cast<int>(first) + static_cast<int>(second);
11 }
12 #endif
13
14
15 int main()
16 {
17     add(true, false);
18 }
```
```

bool to int promotion

Lines 6 - 12 are the crucial ones in this screenshot of C++ Insights². The template instantiation of the function template add creates a full specialization with the return type int. Both bools are implicitly promoted to int.

My belief is that we rely for convenience on the magic of conversions because we don't want to overload a function or reimplement a class for each type.

Let me try the other way and use a generic function. Maybe this is our rescue?

# #### 4.1.1.2 Too Generic

Sorting a container is a general idea. It should work for each container if its elements support ordering. In the following example, I apply the standard algorithm std::sort to the standard container std::list.