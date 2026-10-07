
```cpp
unsigned long power(int i, int k) const;

public:
    FM2(); // default constructor
    ~FM2(); // destructor
    void range(unsigned long seed, int n, double* pu) const;
};

unsigned long FM2::power(int i, int k) const {
    unsigned long iout = (unsigned long)i;
    if (k > 1) {
        iout = iout * power(iout, k - 1);
    }
    return iout;
}

FM2::FM2() {
    a = 63036016;
    expFor2 = 31;
}

void FM2::range(unsigned long seed, int n, double* pu) const {
    unsigned long m = power(2, expFor2) - 1;
    for(int i = 0; i < n; i++) {
        seed = (a * seed) % m;
        pu[i] = (double)seed / (double)m;
    }
}

int main(int argc, char* argv[]) {
    int n = 0;
    unsigned long seed = 0;
    cout << "Choose a value for the sample size:" << endl;
    cin >> n;
    cout << "Choose a value for the seed:" << endl;
    cin >> seed;

    FM2* pm2 = new(std::nothrow) FM2();
    if(pm2 == nullptr) {
        cout << "Memory allocation for pFM2 failed" << endl;
        exit(1);
    }

    double* pu = new(std::nothrow) double[n];
    if(pu == nullptr) {
        cout << "Memory allocation for pu failed" << endl;
        exit(1);
```

# AN FM2 CLASS

Recall from Chapter 3 the C/C++ compiler requires us to provide a sketch prototype information about classes before they can be used. Accordingly, statements 8-9 of Listing 4.2 tell the compiler that FM2 has two data members: a, and an exponent that is to be used in the modulus exp2. The members are declared to have types unsigned long and int, respectively. Statement 10 then gives the prototype for the named recursive function. This function is only used internally in the method range and is therefore designated as private.

The next group of statements (i., 13–14) give two special functions: the class constructor FM2 and the destructor FM2 that are used to create and destroy objects from the class. Finally, a prototype is provided for the actual random number generation function that has been called range. The arguments for this function will be the seed, the sample size n and a pointer to "array" of n double precision locations. The class prototype ends with a semicolon;

The functions or methods that appear in the class (with the exception of the class destructor) are defined in detail next. The compiler is informed that these functions belong to the class FM2 through use of the scope resolution operator ::. The (default) class constructor, the function FM2 sets the value for the constant and the exponent for the modulus in a way that produces the FM2 generator defined as in (4.4). The FM2 class could be structured to provide much more freedom in the creation of a generator by making different choices for a and exp2. This could be incorporated into the class by including an additional constructor that would take its values as arguments (Exercise 4.11), or if the FM2 generator is all we need to use the value of m = 2³−1 could be defined as a global constant to avoid having to (repeatedly) compute it.

The purpose of the destructor is, among other things, to release any memory that has been dynamically allocated in constructing an instance of the class or an object. There is no such commodity that arises in this implementation which means FM2() is just the trivial function with empty body the curly braces. The effect will be that the memory will be deleted whenever an FM2 object goes out of scope. This is actually the behavior for the destructor that is automatically called when none is freed. Consequently, our explicit specification of destructor on line 14 of Listing 4.2 was unnecessary.

To use an object of type FM2 a pointer to the class is created on line 45 of main. In this instance, the new object calls the constructor and allocates this memory which is sufficient to hold all aspects of the resulting FM2. Once this object is available, the range method can be accessed via the -> operator. Lines 46–49 and 51–54 are carried out to show that the memory allocation was successful. If the pointer returned from the version of new is null, in which case an error message will be output, the C++ system function exit (available via <stdlib> header) will be used to immediately terminate the execution of the program.

One possible variation on the design of this class involves allocation of the vector of random numbers. The tactic taken here has been to allocate the memory in main thereby making the process more obvious. One could easily have made the vector of random numbers a private member of FM2. If that destructor would actually need to perform the memory release it would be necessary to add another (const) method that would provide access to the values of random numbers. While Listing 4.2 effectively illustrates the class concept in terms of our "plug-in" code, after all we do not want to copy class prototypes, definitions of methods, etc., into every program where they might be used. The result would be both unwieldy and redundant. Fortunately, this problem can be solved

# GENERATION OF PSEUDO-RANDOM NUMBERS by proceeding as Chapter 3 to break the code into subsegments that are connected to each other as needed include directives for header files. To accomplish this with the FM2.cpp file, a header file FM2.h is created that appears

```cpp
// FM2.h
#ifndef FM2_H
#define FM2_H

class FM2 {
    unsigned long a; // multiplier
    int exp2; // exponent for 2 in modulus
    unsigned long power(int i, int k) const;

public:
    FM2(); // default constructor
    ~FM2(); // destructor
    void range(unsigned long seed, int n, double* pu) const;
};
#endif
```

As was true for the power class in Chapter 3, the FM2.h file essentially consists of just the class prototype that appeared at the beginning of FM2.cpp. The only real difference is the presence of the include guard discussed in Section 3.7. The header file for a class contains all the information that the class does not need to know any of the details about the class methods, e.g., computational methodology, in order to be able to use an object of the class. In fact, the code of the method definitions can be changed without affecting the class interface. This is an important feature in fact that altering the internal aspects of a method (in response to new methodology) will not propagate into other programs that use the class. In addition, casual users of a class need not and, in general, should not alter method definitions. This latter fact is a particularly compelling reason why the actual details of the class will be implemented in a separate source file. As a case in point, the method definitions for the FM2 class will be placed in a file FM2.cpp that has the contents

```cpp
// FM2.cpp
#include "FM2.h"

unsigned long FM2::power(int i, int k) const {
    unsigned long iout = (unsigned long)i;
    if (k > 1) {
        iout = iout * power(i, k - 1);
    }
    return iout;
}

FM2::FM2() : a = 63036016, expFor2 = 31 {}

void FM2::range(unsigned long seed, int n, double* pu) const {
    unsigned long m = power(2, expFor2) - 1;
    for(int i = 0; i < n; i++) {
        seed = (a * seed) % m;
        pu[i] = (double)seed / (double)m;
    }
}
```

# OTHER GENERATION METHODS

The only "new" feature here is the #include statement that brings in the class prototype in FM2. Notice that quotes appear instead of < > telling the preprocessor to look for the header file in the current directory. Finally, the code that actually uses the FM2 class is just the main function in Library 4.2 after having the initial statements

```cpp
#include <iostream>
#include "FM2.h"
#include <new>
using std::cout; using std::cin; using std::endl;
``` e.g., being in the necessary header file. The corresponding code was collected in the file driverFM2.cpp.

At this point the original set of code in Library 4.2 has been split into three distinct parts. By doing this FM2 class has finished with an independent identity that allows it to be employed in other programs. All the pieces are cobbled together in a way that produces an executable program through the use of the myfile below.

```make
driverFM2 : FM2.o driverFM2.o
	g++ -W2 driverFM2.o -o driverFM2

FM2.o : FM2.cpp FM2.h
	g++ -c FM2.cpp
driverFM2.o : driverFM2.cpp FM2.h
	g++ -Wall -c driverFM2.cpp
```

This produces the executable driverFM2 that can be used, as before, to obtain from the program. Tauswort (1965) proposed a class of random number generators that are referred to as linear feedback shift register generators. Although these particular generators are not held in high regard, their extensions are widely used and provide some of what are arguably the best generators that are currently available.
