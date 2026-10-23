```
```cpp
#include <cstdlib>
#include <random>

namespace Distributions
{
    double DISTRIBUTIONLIBRARY_API PdfNormal(double x);   // n(x)

    double DISTRIBUTIONLIBRARY_API CdfNormal(double x);   // N(x)

    class NormalDistribution
    { // Test case
      private:
        std::default_random_engine eng;
        std::normal_distribution<double> nor;

      public:
        DISTRIBUTIONLIBRARY_API NormalDistribution(double a=0.0,
        double b=1.0);

        // Generate normal(a,b) normal variate
        DISTRIBUTIONLIBRARY_API double rng();

        // Create an array of normal variates
        DISTRIBUTIONLIBRARY_API std::vector<double> rngArray(long n);

        // Create an array of normal variates and shuffle them
        DISTRIBUTIONLIBRARY_API std::vector<double> rngShuffledArray
                                      (long n);

        // Create an array by Mersenne Twister
        DISTRIBUTIONLIBRARY_API std::vector<double> rngMTArray(long n);
    };
}
```
```

The keyword `__declspec(dllexport)` provides a means to *export* functions from an .exe or .dll file whereas programs that use public symbols defined by a DLL use the keyword `__declspec(dllimport)` to import them. The code file and test program are the same as in Section 8.7.1.1.

Finally, we discuss how to create a DLL library in Visual Studio (a discussion of how to do this for other compilers is outside the current scope). The main steps are: (1) create a DLL project; (2) add classes to the DLL library; (3) build the project to produce a .dll file; (4) create a Console executable project, reference the DLL library and use its functionality in the main method. For more specific details, see the Microsoft online documentation.

On a technical note, we make the .dll file visible to the .exe by copying the .dll to the same directory where the .exe file resides or by placing the DLL project in the .exe’s solution project.

It is possible to create DLLs using *module-definition* files but a discussion is outside the current scope. See Rogerson (1997).