```
```cpp
// execute algorithm:
std::cerr << "---[ Start std::sort() ]--------------------\n";
std::sort<>( &input[0], &input[9]+1);
std::cerr << "---[ End std::sort() ]----------------------\n";

// verify result:
for (int i=0; i<10; ++i) {
    std::cerr << input[i].val() << ' ';
}
std::cerr << "\n\n";

// final report:
std::cerr << "std::sort() of 10 SortTracer’s"
          << " was performed by:\n "
          << SortTracer::creations() - created_at_start
          << " temporary tracers\n "
          << "up to "
          << SortTracer::max_live()
          << " tracers at the same time ("
          << max_live_at_start << " before)\n "
          << SortTracer::assignments() - assigned_at_start
          << " assignments\n "
          << SortTracer::comparisons() - compared_at_start
          << " comparisons\n\n";
}
```
```