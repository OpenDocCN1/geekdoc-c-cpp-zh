```
while (source_it != source.end()) {
    auto s_it = source_it++;
    vec_mst.push_back(my_special_type{*s_it,
*s_it});
}
}
```

In an unoptimized build this will create a temporary object and invoke push_back(my_special_type&&), allowing the move constructor to be used rather than the copy con-structor. But we can go even further by using emplace_back:

Click here to view code image

```
void accumulate_mst(std::vector<my_special_type>&
vec_mst,
                    std::vector<int> const&
source) {
    auto source_it = source.begin();
    while (source_it != source.end()) {
        auto s_it = source_it++;
        vec_mst.emplace_back(*s_it, *s_it);
    }
}
```

> > *Declaring at point of use improves readability of code, and not declaring state at all improves things even further. Reasoning about state requires a comprehensive memory, which is a diminishing asset as codebases expand.*

We have eliminated some state from the function. Now, you may think that you have improved the performance of your program by doing this. However, each of those functions does the same thing, and the compiler will probably generate the same assembly for each. In the first example the