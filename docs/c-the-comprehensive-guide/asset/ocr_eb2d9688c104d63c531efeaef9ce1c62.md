```
```cpp
// With letters it becomes even clearer
std::string x = "abddggi";
std::string y = "BBCDDH";
using Us = std::ostream_iterator<char>;    // Type of output iterator
Us us{std::cout, ""};                      // Stream output for char
auto compare = [](auto c, auto d) { return toupper(c) < toupper(d); };
auto run2 = [&x,&y,&us,&compare](auto algo) {    // use x,y, and us
    algo(x.begin(), x.end(), y.begin(), y.end(), us, compare);
    std::cout << '\n';
};
// Results of the algorithms
using It = decltype(x.begin());             // Type of input iterators
using Cm = decltype(compare);               // Type of comparison function

run2(std::merge<It,It,Us,Cm>);              // Output: abBBCdddDDggHi
run2(std::set_union<It,It,Us,Cm>);          // Output: abBCddggHi
run2(std::set_intersection<It,It,Us,Cm>);   // Output: bdd
run2(std::set_difference<It,It,Us,Cm>);     // Output: adggi
run2(std::set_symmetric_difference<It,It,Us,Cm>); // Output: aBCddgHi
}
```
```

Listing 25.14  Functionality of the set algorithms.

I sequentially apply the set algorithms that have two input sets and one output set. This happens in the run and run2 lambdas. If you do not specify a comparison function—shown in run—then it will compare based on <. For the second example, I defined a comparison operator that ignores case sensitivity. This way, you can see in the results which original set each output character comes from:

+   - **merge**  
+     Usage: frequent; iterators: in/out  
+     Merges two sorted ranges into a new sorted range.
+   - **inplace_merge**  
+     Usage: occasional; iterators: bi  
+     Like merge, but assumes the ranges are adjacent.
+   - **includes**  
+     Usage: occasional; iterators: in  
+     Checks if set B is a subset of set A.
+   - **set_union**  
+     Usage: occasional; iterators: in/out  
+     Merges two containers, A and B; duplicates in B are retained; skips elements in B that are present in A.