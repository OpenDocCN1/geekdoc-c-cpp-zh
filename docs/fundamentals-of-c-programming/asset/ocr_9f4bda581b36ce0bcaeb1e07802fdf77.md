and
1,045 = 11,045 = 21,045 = 31,045

Since the rand function cannot produce any values in the range 32,678...39,999, the rightmost column is not complete. Because the leftmost three columns are complete, the modulus operator can produce values in the range 0...2,767 four different ways; for example, the following code fragment

```
std::cout << 5 % 10000 << ' ' << 10005 % 10000 << ' ' <<
<< 20005 % 10000 << ' ' << 30005 % 10000 << '\n';
```

prints

```
5 5 5 5
```

The rand function cannot return a value greater than 32,767; specifically, in our program above, rand cannot produce 39,995. Listing 13.9 (badrand.cpp), therefore, using rand and modulus we can produce 9,995 in only three different ways: 9,995, 19,995, and 29,995. Based on our analysis, Listing 13.9 (badrand.cpp) can generate the number 5 four different ways and 9,995 three different ways. This 4:3 ratio agrees with our empirical observations of the behavior of Listing 13.9 (badrand.cpp). The consequences of this bias means that values in the relatively small range 0...2,767 will appear disproportionately more frequently than numbers in the larger range 2,768...9,999. Such bias definitely is undesirable in a pseudorandom number generator.

We must use more sophisticated means to produce better pseudorandom numbers. Fortunately C++11 provides several standard classes that provide high-quality pseudorandom generators worthy of advanced scientific and mathematical applications.

The rand function itself has another weakness that makes it undesirable for serious scientific, engineering, and mathematical applications. rand uses a linear congruential generator algorithm (see http://en.wikipedia.org/wiki/Linear_congruential_generator). rand has a relatively small period. This means that the pattern of the sequence of numbers it generates will repeat itself exactly if you call rand enough times. For Visual C++, rand's period is 2,147,483,648. Listing 13.10 (randomperiod.cpp) verifies the period of rand.

# Listing 13.10: randomperiod.cpp

```
#include <iostream>
#include <iomanip>
#include <cstdlib>
#include <ctime>

int main() {
  // Set random number seed value
  srand(42);

  // Need to use numbers larger than regular integers; use long long ints
  for (long long i = 1; i < 4294967400LL; ++i) {
    int r = rand();
    if (1 <= i && i <= 10)
      std::cout << std::setw(10) << i << " : " << std::setw(6) << r << '\n';
    else if (2147483645 <= i && i <= 2147483658)
      std::cout << std::setw(10) << i << " : " << std::setw(6) << r << '\n';
    else if (4294967293LL <= i && i <= 4294967309LL)
      std::cout << std::setw(10) << i << " : " << std::setw(6) << r << '\n';
  }
}
```