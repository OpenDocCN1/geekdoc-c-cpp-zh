However, it is even more important that you have to perform a few
calulations as possible. Let's assume you work in video editing and
want to calculate the length of a movie. Videos often have one frame
per 1/25 of a second. Then you can calculate the current movie time in
a loop in two ways. First, try it accumulated, and second, try it with
closed multiplication, as the following listings demonstrate.

```
// https://godbolt.org/z/SEEp9bH5K
#include <iostream> // setprecision, fixed
constexpr int framesPerSec = 25;
constexpr int runtimeInSec = 3600;
constexpr int framesTotal = runtimeInSec * framesPerSec;
constexpr float frametime = 1.0 / framesPerSec;

int main() {
    float filetime = 0.f;
    for(int n=0; n < framesTotal; ++n) {
        filetime += frametime; // accumulate
    }
    std::cout << std::precision(10) << std::fixed
              << filetime << "\n"; // output: 3602.2605312500
}
```

# **Listing 4.36** Accumulated time measurement.

You shouldn't be surprised that more than two seconds of errors have
accumulated in one hour of film.

# Labeling Constants

For constexpr, refer to Chapter 13, Section 13.10.6. It is
advantageous for the compiler and for you if you mark\unchangeable values (i.e., constants) as such. You can use (static)
const or constexpr for this purpose. The latter ensures that the
compiler can calculate the constant in advance. If it cannot do this,
it will inform you accordingly.

Let the loop run from 1 to <= framesTotal to be able to compare it better
with the next example.

However, you can also approach this differently. So long as the
frametime remains constant over the course of the movie, you can
calculate it in one step. So you are scaling as in in the following listing.