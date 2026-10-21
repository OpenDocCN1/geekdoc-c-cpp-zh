```
```cpp
std::plus{}, twice);

std::cout << "\n transform_inclusive_scan():     ";
std::transform_inclusive_scan(coll.begin(), coll.end(),
                              std::ostream_iterator<int>(std::cout, " "),
                              std::plus{}, twice, 100);

std::cout << "\n transform_exclusive_scan(): ";
std::transform_exclusive_scan(coll.begin(), coll.end(),
                              std::ostream_iterator<int>(std::cout, " "),
                              100, std::plus{}, twice); // note the other param order
}
```
```

has the following output:

```
```
source:                         3 1 7 0 4 1 6 3
transform_inclusive_scan():       6 8 22 22 30 32 44 50
transform_inclusive_scan():       106 108 122 122 130 132 144 150
transform_exclusive_scan():       100 106 108 122 122 130 132 144
```
```

Note that both algorithms always output the same number of elements that the input range has. However, with `transform_inclusive_scan()`, we start with the transferred value of the first element and end with the sum/combination of all transferred element values (plus any passed initial value used as offset), while with `transform_exclusive_scan()`, we start with the initial value and end with the sum/combination of the transferred values of all but the last element.

# 23.3 Afternotes

for_each_n(), the ...reduce(), and the ...scan() algorithms were first proposed with the general proposal of the parallelization of the STL algorithms in 2012 by Jared Hoberock, Michael Garland, Olivier Giroux, Vinod Grover, Ujval Kapasi, and Jaydeep Marathe in http://wg21.link/n3408. It became a formal beta standard, the Technical Specification for C++ Extensions for Parallelism (see http://wg21.link/n3850). Additional transform...scan() forms were added by Jared Hoberock, Grant Mercer, Agustin Berge, and Harmut Kaiser in http://wg21.link/n4276. With http://wg21.link/p0024r2, the Technical Specification for C++ Extensions for Parallelism was adopted to the standard library as proposed by Jared Hoberock. The handling of exceptions was accepted as proposed by JF Bastien and Bryce Adelstein Lelbach in http://wg21.link/p0394r4.