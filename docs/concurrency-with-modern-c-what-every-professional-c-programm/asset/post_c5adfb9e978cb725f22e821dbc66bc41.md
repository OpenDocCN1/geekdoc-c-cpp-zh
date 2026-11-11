
```cpp
// transform_exclusive_scan and transform_inclusive_scan
std::vector<int> resVec3{1, 2, 3, 4, 5, 6, 7, 8, 9};
std::vector<int> resVec4(resVec3.size());
std::transform_exclusive_scan(std::execution::par,
                               resVec3.begin(), resVec3.end(),
                               resVec4.begin(), 0,
                               [](auto fir, int sec){ return fir + sec; },
                               [](auto arg){ return arg * arg; });

std::cout << "transform_exclusive_scan: ";
for (auto v: resVec4) std::cout << v << " ";
std::cout << "\n";

std::vector<std::string> strVec{"Only","for","testing","purpose"};
std::vector<int> resVec5(strVec.size());

std::transform_inclusive_scan(std::execution::par,
                               strVec.begin(), strVec.end(),
                               resVec5.begin(),
                               [](auto fir, auto sec){ return fir + sec; },
                               [](auto s){ return s.length(); }, static_cast<std::size_t>(0));



std::cout << "transform_inclusive_scan: ";
for (auto v: resVec5) std::cout << v << " ";
std::cout << "\n";

// reduce and transform_reduce
std::vector<std::string> strVec2{"Only","for","testing","purpose"};

std::string res = std::reduce(std::execution::par,
                               strVec2.begin() + 1, strVec2.end(), strVec2[0],
                               [](auto fir, auto sec){ return fir + ":" + sec; });

std::cout << "reduce: " << res << '\n';

auto res7 = std::transform_reduce(std::execution::par,
                               strVec2.begin(), strVec2.end(), static_cast<std::size_t>(0),
                               [](auto a, auto b){ return a + b; },
                               [](std::string s){ return s.length(); });


std::cout << "transform_reduce: " << res7 << '\n';
std::cout << '\n';

}
```

I apply the new algorithms to a `std::vector<int>` (line 17) and a `std::vector<std::string>` (line 58). The `std::for_each_n` algorithm in line 18 maps the first n ints of the vector to their squares.

`std::exclusive_scan` (line 27) and `std::inclusive_scan` (line 37) are quite similar. Both apply a binary operation to their elements. The difference is that `std::exclusive_scan` excludes the last element in each iteration.

The `std::transform_exclusive_scan` in line 48 is quite challenging to read. Let me try to explain it. In the first step I apply the lambda function `[](int arg){ return arg * arg; }` to each element of the range `resVec3.begin()` to `resVec3.end()`. In the second step, I apply the binary operation `[](int fir, int sec){ return fir + sec; }` to the intermediate vector. This means, sum up all elements using 0 as the initial value. The result is placed in `resVec4.begin()`.

The `std::transform_inclusive_scan` function in line 61 is similar. This function maps each element to its length.

The `std::reduce` function should be pretty easy to read; it puts ":" characters between every two elements of the input vector. The resulting string should not start with a ":" character; therefore, the range starts at the second element (`strVec2.begin() + 1`) and uses the first element of the vector `strVec2[0]` as the initial element.

![](img/d61a6c83410484053b8892275d2fcc4f_257_0.png)

## transform_reduce becomes map_reduce

I have more to say about the `std::transform_reduce` function in line 80. First of all, the C++ algorithm transform is in other languages often called map. Therefore, we could also call `std::transform_reduce` `std::map_reduce`. Now I assume you noticed it. `std::transform_reduce` is the well-known parallel MapReduce* algorithm implemented in C++. Accordingly, `std::transform_reduce` maps a unary callable (`[](std::string s){ return s.length(); }`) onto a range and reduces the pair to an output value: `[](std::size_t a, std::size_t b){ return a + b; }`.

Studying the output of the program should help you.

> *https://en.wikipedia.org/wiki/MapReduce*

- `foldl` and `foldl1` apply a binary operation to a list and reduce the list to a value. `foldl` needs, in contrast to `foldl1`, an initial value. `foldl1` requires the list to be non-empty and uses the first element as the initial value.
- `scanl` and `scanl1` apply the same strategy such as `foldl` and `foldl1`, but they produce all intermediate results so that you get back a list.
- `foldl`, `foldl1`, `scanl`, and `scanl1` start their job from the left.

Let’s have a look at the Haskell functions. Here is Haskell’s interpreter shell.

![](img/d61a6c83410484053b8892275d2fcc4f_259_0.png)

New algorithms in Haskell

(1) and (2) define a list of integers and a list of strings. In (3), I apply the lambda function `(\a -> a * a)` to the list of integers. (4) and (5) are more sophisticated. The expression (4) multiplies `(*)` all pairs of integers starting with the one as the neutral element of multiplication. Expression (5) does the corresponding for addition. Expressions (6), (7), and (9) are quite challenging for the imperative programmer. You have to read them from right to left. `scanl (+) . map (\a -> length a)` (7) is a function composition. The dot `(.)` symbol composes the two functions. The first function maps each element to its length; the second function adds the list of lengths together. (9) is similar to (7). The difference is that `foldl` produces one value and requires an initial element, that is in this case 0. Now expression (8) should be readable; it successively joins two strings with the `:` character.

```cpp
func();
const std::chrono::duration<double> dur = std::chrono::steady_clock::now() - sta;
std::cout << " " << dur.count() << " sec." << '\n';

}

int main(){

    std::cout << '\n';

    std::vector<double> randValues;
    randValues.reserve(size);

    std::mt19937 engine;
    std::uniform_real_distribution<> uniformDist(0, pi / 2);
    for (long long i = 0; i < size; ++i) randValues.push_back(uniformDist(engine));

    std::vector<double> workVec(randValues);

    getExecutionTime("std::execution::seq", [workVec]() mutable {
        std::transform(std::execution::seq, workVec.begin(), workVec.end(),
                       workVec.begin(),
                       [](double arg) { return std::tan(arg); }
        );
    });

    getExecutionTime("std::execution::par", [workVec]() mutable {
        std::transform(std::execution::par, workVec.begin(), workVec.end(),
                       workVec.begin(),
                       [](double arg) { return std::tan(arg); }
        );
    });

    getExecutionTime("std::execution::par_unseq", [workVec]() mutable {
        std::transform(std::execution::par_unseq, workVec.begin(), workVec.end(),
                       workVec.begin(),
                       [](double arg) { return std::tan(arg); }
        );
    });

    std::cout << '\n';
}
```

*unsequenced policies the same way, so you should not expect better performance for using par_unseq on our implementation, but implementations may exist that can use that additional freedom someday.*

### 4.5.2 GCC Compiler

My Linux computer has only four cores. Here are the numbers.

![](img/d61a6c83410484053b8892275d2fcc4f_264_0.png)

Sequential, parallel, and parallel and vectorized execution using the GCC Compiler

The numbers are as expected. I have four cores and the parallel execution is about four times faster than the sequential execution. The performance numbers of the parallel and vectorized version and the parallel version are in the same ballpark. My assumption is, therefore, that the GCC compiler uses the same strategy such as the Windows compiler. When I ask for the parallel and vectorized execution by using the execution policy `std::execution::par_unseq`, I get the parallel execution policy (`std::execution::par`). This behavior is according to the C++17 standard because the execution policies are only a hint for the compiler.

### Distilled Information

- With C++17, most of the STL algorithms are available in a parallel implementation. This makes it possible to invoke an algorithm with a so-called execution policy. This policy specifies whether the algorithm runs sequentially, in parallel, or in parallel with additional vectorization.
- Additionally to the 69 algorithms available in overloaded versions for parallel or parallel and vectorized execution, we get new algorithms. These new ones are well suited for parallel reducing, scanning, or transforming ranges.
