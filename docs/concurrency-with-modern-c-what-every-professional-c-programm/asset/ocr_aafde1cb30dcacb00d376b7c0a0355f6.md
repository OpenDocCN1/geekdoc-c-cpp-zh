```
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
```
```