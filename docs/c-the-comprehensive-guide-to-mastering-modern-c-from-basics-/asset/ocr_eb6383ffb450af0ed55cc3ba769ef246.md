```
docker run --rm -it --volume $(pwd):/workdir --workdir /workdir gcc13 \
./GCC-25AlgoPar.x
```

```
// https://godbolt.org/Koxoha5bxx
#include <algorithm> // find
#include <numeric> // reduce, accumulate
#include <execution> // std::execution
#include <iostream>
#include <chrono> // time measurement
using namespace std::chrono;
long long millisecond(steady_clock::time_point start) {
    return duration_cast<milliseconds>(steady_clock::now()-
        start).count();
}

template<typename FUNC> void timeit(const char* title, FUNC func) {
    auto start = steady_clock::now();
    auto ret = func(); // execute
    std::cout << title << ": " << millisecond(start) << " ms" << std::endl;
    std::endl;
}
int main() {
    using namespace std::execution; // seq, par, par_unseq
    using std::reduce; using std::accumulate; using std::find;
    std::vector<double> v(600 000 000, 0.0); // 600 million elements
    for(auto& x) x = rand(); // fill with random values
    timeit("warm-up", [&] {
        return reduce(seq, v.begin(), v.end(), 0.0);
    });
    timeit("accumulate", [&] {
        return accumulate(v.begin(), v.end(), 0.0);
    });
    timeit("reduce", [&] {
        return reduce(seq, v.begin(), v.end(), 0.0);
    });
    timeit("reduce", [&] {
        return reduce(par, v.begin(), v.end(), 0.0);
    });
    timeit("par, unseq", [&] {
        return reduce(par_unseq, v.begin(), v.end(), 0.0);
    });
    timeit("find, seq", [&] {
        return find(seq, v.begin(), v.end(), 1.1) == v.end() ? 0.0 : 1.0;
    });
    timeit("find, par", [&] {
        return find(par, v.begin(), v.end(), 1.1) == v.end() ? 0.0 : 1.0;
    });
}
```