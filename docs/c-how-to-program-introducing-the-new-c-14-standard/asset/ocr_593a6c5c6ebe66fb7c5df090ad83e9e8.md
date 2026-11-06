`array`, or O(*n*) comparisons total. This pattern continues, as each level works on twice as many `array`s, but each is half the size of the previous `array`.

+   - Similar to binary search, this halving results in log *n* levels, each level requiring O(*n*) comparisons, for a total efficiency of **O(*n* log *n*)** (p. 861).