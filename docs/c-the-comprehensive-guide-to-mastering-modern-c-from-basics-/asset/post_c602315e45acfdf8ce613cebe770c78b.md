
readable from the start.

Assume you have numerous messages like this:

score 400 for 2 nights at Minas Tirith Airport

Here, the texts and numbers can change. You are supposed to extract the numbers 400 and 2 as well as the hotel name, Minas Tirith Airport, after at. The regular expression can look like this:

```cpp
const string pattern = R"(\^\s+(\d+)\s+for\s+(\d+)\s+nights?\s+at\s+(.*))";
```

In the program, it looks like the following listing.

```cpp
// https://godbolt.org/z/dg5ve3heM
#include <regex>
#include <string>
#include <iostream>
using std::regex; using std::regex_search; using std::cmatch;
const regex pattern(R"(\^\s+(\d+)\s+for\s+(\d+)\s+nights?\s+at\s+(.*))");
void extract(const std::string& text, const regex& pattern) {
  cmatch res;
  regex_search(text.c_str(), res, pattern);
  std::cout << res[1] << " " << res[2] << " " << "\n";
}

int main() {
  extract("score 400 for 2 nights at Minas Tirith Airport");
  extract("score 84 for 1 night at Prancing Pony");
}
```

## Listing 28.14 Hard to maintain regular expression.

This is still readable. To improve readability, always there are at least three options:

- Restructure
- Use descriptive names
- Comment

Combining the first two approaches, you could perhaps break down the regex into several smaller ones, give the parts names, and then combine them.

```cpp
// https://godbolt.org/z/TK6n4dG37
const string scoreKeyword = R"(score\s+)";
const string numberOfPoints = R"(\d+)";
const string forKeyword = R"(for\s+)";
const string numberOfNights = R"(\d+)";
const string nightsAtKeyword = R"(\snights?at\s+)";
const string hotelName = R"(\.*)";
const regex pattern(scoreKeyword + numberOfPoints + forKeyword + numberOfNights + nightsAtKeyword + hotelName);
```

## Listing 28.15 Name parts and then combine them.

Perhaps this is more maintainable. At least this approach is recommended if parts of the expression might be used elsewhere in the program.

The third approach to commenting also works, except that C++ comments within the expression—within the string—do not work.

Here you can use the feature that C++ directly concatenates adjacent string literals if only whitespaces remain after removing them. In this way, you can then comment parts of the expression in an almost "embedded" way.

```cpp
// https://godbolt.org/z/MszTjE3dv
const regex pattern(R"(score)"
R"(\s+)"
R"(\d+)" // points
R"(\s+)"
R"(for)"
R"(\s+)"
R"(\d+)" // number of nights
R"(\s+)"
R"(night)"
R"(\s+)" // optional: plural
R"(\s+)"
R"(at)"
R"(\s+)"
R"(\{.*\})" // hotel name
R"(\))");
```

## Listing 28.16 Commenting within the expression.

All raw string fragments R"(...)" are directly adjacent, ignoring whitespaces and comments. The C++ preprocessor combines these into a single string literal.

## 28.3 Randomness

True random numbers are a difficult thing for computers. But in some applications, you need good random numbers. And the good old `rand()` from `<cstdlib>` no longer suffices—or `<cstdlib>`, as the header is called in the C11 standard. Even in the standard document, you can read about `rand()`: “There are no guarantees as to the quality of the random sequence produced and some implementations are known to produce sequences with disturbingly non-random low-order bits. Applications with particular requirements should use a generator that is known to be sufficient for their needs.” Or, in short: If you value randomness do not use `rand()`! Instead use `<random>`, because according to Bjarne Stroustrup, “what random number library wants to be.”

In C++, the `<random>` header provides everything you need for random number generation. For 99% of all applications, the provided functionalities should suffice. You may build upon classes and add your own extensions if necessary. However, I also mention that `<random>` does not cater to cryptography. For these applications, you will need third-party libraries, and you can use `<random>` as inspiration.

If you just want to simulate a die with many sides it is not really complicated. But if you are a physicist or mathematician and know that you need a random number with a certain performance then you need to dig deeper, but you will still find what you need in `<random>`. This part of the library offers something for every level:

- Occasional users: A preconfigured generator and two distributions
- Intermediate and advanced users: Nine generators, more distributions, a true number generator, and a helper class
- Experts: Six configurable adapters for generators and a function template for writing custom distributions

For average users who want to get a uniformly distributed number, the next likes simple:

```cpp
// https://godbolt.org/z/ocP8a7ac
#include <random>
#include <vector>
#include <iostream>
void rollDice() {
  std::default_random_engine engine(); // Normal randomness
  std::vector<size_t> counts({0,0,0,0,0});
  std::uniform_distribution<int> d(0, 5); // uniformly distributed integers
  for(auto i=120*1000; i>0; --i)
    ++counts[d(engine)];
  for(auto c : counts) std::cout << "\n";
}

int main() {
  rollDice();
}
```

## Listing 28.17 This is how you get a uniformly distributed number between two bounds.

The output is the number of times each number was rolled. If all numbers were rolled equally often you would see something else but instead this: 199664 200248 199727 200143 200373 199845 you can see generating random numbers consists of two things:

- Engine: The "engine" is responsible for generating the (possibly pseudo)random bits. Different generators produce random numbers with different qualities and at different speeds.
- Distribution: The distribution is responsible for mapping the bit representation to the actual numbers to be generated. These can be uniformly distributed within a certain range, clustered at specific points, and so on.

If you combine these two things you get the random number generator. A distribution like ds defines the operator() call. If you pass an engine as an argument to it, you get a random number of the desired quality, as per the preceding example:

```cpp
auto number = d(engine);
```

And number is now between 0 and 5 (inclusive) with equal probability. If you don't like having to always carry and specify the engine here simply combine both into a function object—for example, with a lambda:

```cpp
auto d = [&]() { return d(engine); };
std::cout << d() << '\n';
```

And when I run Listing 28.17 again, I get the output. And again and again—that's a very unlikely coincidence, isn't it? It would be indeed, but all engines (except one which we will get to shortly) are pseudorandom number generators: initialized with the same seed, they always produce the same bit sequence—which looks random under certain considerations and is sufficient for many (most?) applications. The reason I always got the exact sequence of pseudorandom numbers is that I always chose the same seed for the engine—namely, the default value. You can pass a different seed as a constructor argument:

```cpp
std::default_random_engine engine(42);
std::default_random_engine engine(806699);
std::default_random_engine engine(time(0)); // from <ctime>
```

Each seed value provides a different pseudo-random sequence. If you start with a variable value—like here with time(0), the current time—you will always get a different sequence. This is sufficient for standard cases. If you need more, there is the std::seed_seq helper class.

However, it may be that you get a different sequence of pseudorandom numbers on your machine than I do. Even though the generators are all well-defined by the standard, the default_random_engine is mapped to one of the generators by your specific implementation; which one is decided by the manufacturer. If you need reproducibility, set both the generator and the seed value.

## 28.3.2 True Randomness provided by the random_device generator.

This does not derive randomness from a seed and a mathematical formula but from various randomness-producing components of your computer, such as mouse movements or hard disk head movements. However, this generator has a few significant disadvantages:

- It is slow. Especially on server systems (without a mouse and the like), it is sometimes very slow.
- Results are not reproducible, for example, for debugging; thus the advantage can turn into a disadvantage.
- The C++ implementation does not have to offer this engine; it is optional.

You can check with the entropy() function of random_device whether random_device can really generate
