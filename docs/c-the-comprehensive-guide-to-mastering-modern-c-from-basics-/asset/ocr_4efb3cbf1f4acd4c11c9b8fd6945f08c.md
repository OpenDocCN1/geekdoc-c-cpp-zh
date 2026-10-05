So if you have the optimal numerical application and are on a type of CPU with a given compiler, then valarray might be the right choice.

Check if the *mdspan* added in C++23 is useful for you. Then you can write `cube[3,5,7]` because the operator[] also supports multidimensional indices since C++23!

With C++26, chances are that Basic Linear Algebra Subroutines (BLAS) will become part of the standard. Those would be in the `<linalg>` header and would allow you much more than matrix multiplication. They even come with parallel execution policies.

For a valarray<T>, 24.12.1 Element Properties should be a numeric data type. I

recommend a built-in integer or floating-point type. Also, `complex<>` may be suitable under certain circumstances. The most useful valarray can be if T supports arithmetic, bitwise, and/or Boolean operations (as int would)—the more, the better. T is perfect if it supports trigonometric functions and the like, as double would.

| Container | Description |
| --- | --- |
| valarray<T> | Not compatible with other containers; for fast processing of numerical data in one or more dimensions |
| slice | Selected range of a valarray |