
## 46. Use the Tools: Multiple Compilers

Support *at least* 2 compilers on your platform. Each compiler does different analyses and implements the standard in a slightly different way.

If you use Visual Studio, you should be able to switch between clang and cl.exe relatively easily. You can also use WSL and enable remote Linux Builds.

If you use Linux, you should be able to switch between GCC and Clang easily.

On MacOS, be sure the compiler you are using is what you think it is. gcc command is likely a symlink to clang installed by Apple.

For installing newer or different compilers on your platform, the following is available:

Ubuntu / Debian

- GCC - Toolchain PPA¹
- Clang - apt packages²

Windows

- GCC MinGW³
- Clang official downloads⁴

MacOS

- Homebrew / MacPorts

¹ https://launchpad.net/~ubuntu-toolchain-r/+archive/ubuntu/ppa
² https://apt.llvm.org/
³ https://mingw.org/
⁴ https://releases.llvm.org/download.html

### Exercise: Add Another Compiler

Since you have already enabled continuous builds of your system, it's time to add another compiler.

A new version of the compiler you currently require is always a good idea. But if you only support GCC, consider adding Clang. Or if you only support Clang, add GCC. If you're on Windows, add MinGW or Clang in addition to MSVC.

### Exercise: Add Another Operating System

Hopefully, at least some portion of your project can be ported to another operating system. The exercise of getting parts of the project compiling on another operating system and toolchain will teach you a lot about your code's nature.

### Resources

- C++Now 2015: Jason Turner “Thinking Portable: How and Why to make your C++ Cross Platform”^5

^5 https://youtu.be/cb3WIL96N-o

## 47. Fuzzing and Mutating

Your imagination limits the tests that you can create. Do you try to be malicious when calling your APIs? Do you intentionally pass malformed data to your inputs? Do you process inputs from unknown or untrusted sources?

Generating all possible inputs to all possible function calls in all possible combinations is impossible. Fortunately, tools exist to solve this problem.

### Fuzzing

Fuzz testers generate strings of random data of various lengths. The test harness you write consumes these strings of data and processes them in some way that is appropriate for your application. The fuzz tester analyzes coverage data generated from your test’s execution and uses that information to remove redundant tests and generate new novel and unique tests.

In theory, a fuzz test will eventually reach 100% code coverage of your tested code, if left to run long enough. Combined with AddressSanitizer, this makes a powerful tool for finding bugs in your code. [One interesting article from 2015](https://blog.hboeck.de/archives/868-How-Heartbleed-couldve-been-found.html) describes how the combination of a fuzz tester and AddressSanitizer could have found the security flaw “heartbleed” in OpenSSL in less than 6 hrs.

![](img/60cb742bacdfc38724280b0dae4597e3_113_0.png)

Fuzz testing primarily finds memory and security flaws.

Many different fuzzing tools exist. For the sake of this section, I am going to cover only [LLVM’s libFuzzer](https://llvm.org/docs/LibFuzzer.html). All fuzz testers operate under the same premise.

You must provide some sort of entry point. The entry point generally takes the form of a function like:

```cpp
// tested in a real test
auto [newDataPtr, remainingSize, Obj1]
  = createStruct<Type1>(Data, Size);
auto [lastDataPtr, lastSize, Obj2]
  = createStruct<Type2>(newDataPtr, remainingSize);

functionToTest(Obj1, Obj2);
}
```

¹ https://blog.hboeck.de/archives/868-How-Heartbleed-couldve-been-found.html
² https://www.llvm.org/docs/LibFuzzer.html

The fuzzer will quickly learn that any new data input where Size > sizeof(Type1) + sizeof(Type1) does not generate new code paths and will focus on the appropriate amount of data.

### Mutating

Mutation testing works by modifying conditionals and constants in the code being tested.

*Pseudo code example.*

```cpp
bool greaterThanFive(const int value) {
    return value > 5; // comparison
}

void tests() {
    assert(greaterThanFive(6));
    assert(!greaterThanFive(4));
}
```

A mutation tester could modify the constant 5 or the > so the resulting code might become

*Mutated code.*

```cpp
bool greaterThanFive(const int value) {
    return value < 5; // mutated
}
```

Any test that continues to pass is a “mutant that has survived” and indicates either a flawed test or a bug in the code.

### Exercise: Create a fuzz test harness.

Apply the examples demonstrated here to create fuzz testers for your code. What challenges do you hit?

Look at FuzzedDataProvider.h³ for more helper functions

### Exercise: Investigate mutation testing.

The author of this book has no direct experience with mutation testing. Is it something you can use in your project? What interesting resources do you find?

### Resources

- C++Now 2018: Marshall Clow “Making Your Library More Reliable with Fuzzing”⁴
- C++ Weekly Ep 85: Fuzz Testing⁵
- CppCast: Alex Denisov “Mutation Testing With Mull”⁶
- NDC TechTown 2019: Seph De Busser “Testing The Tests: Mutation Testing for C++”⁷
- CppCon 2017: Kostya Serebryany “Fuzz or lose…”⁸
- CppCon 2020: Barnabás Bágyi “Fuzzing Class Interfaces for Generating and Running Tests with libFuzzer”⁹ - Inspirational talk about using fuzzing in novel ways. Video is not yet on YouTube, but look for it after this book is published.
- Autotest¹⁰ - Library associated with “Fuzzing Class Interfaces for Generating and Running Tests with libFuzzer” talk.

⁵ https://youtu.be/gOOKBoqKoOU
⁶ https://cppcast.com/alex-denisov/
⁷ https://youtu.be/M-5_M8qZXaE
⁸ https://youtu.be/k-Cv8Q3zWNQ
⁹ https://cppcon2020.sched.com/event/e7An/fuzzing-class-interfaces-for-generating-and-running-tests-with-libfuzzer?iframe=no
¹⁰ https://gitlab.com/wilzegers/autotest/

Many of those conferences and user groups are now meeting online. It's now possible for us to all attend each other's user groups. [The North Denver Metro C++ Meetup](https://www.meetup.com/North-Denver-Metro-C-Meetup/)^4^, for example, regularly has one attendee from Thailand each month.

^4^ https://www.meetup.com/North-Denver-Metro-C-Meetup/

### C++ Weekly

This book references C++ Weekly throughout as a resource to go back to for more information and examples to share with your coworkers. At this moment, the show has been going for 235 weeks straight with many special editions, extras, and live streams.

### cppreference.com

The website is fantastic, but you might not know that you can create an account and customize the content to the version of C++ you are using. Also, you can [execute examples](https://en.cppreference.com/w/Cppreference) and [download an offline version](https://en.cppreference.com/w/Cppreference)^5^

^5^ https://en.cppreference.com/w/Cppreference

### Hire a Trainer to Come Onsite for Your Company

Team training gets your team thinking in a new direction, improves morale, and boosts employee retention. Since you made it this far, I'm going to offer you a coupon.

If you mention this book, you'll get 10% off onsite training costs at your company from me. (travel costs not discounted). Hopefully, travel restrictions will not last much longer.

### YouTube

- Andreas Fertig’s Channel⁶
- C++ Weekly (Author’s Channel)⁷
- CopperSpice⁸

⁶ https://www.youtube.com/channel/UCxJfSPGHFS3_nRDv1u-Q8g
⁷ https://www.youtube.com/c/JasonTurner-lefticus
⁸ https://www.youtube.com/copperspice

## 49. Thank You

### Sponsors

Thank you to all of my Book Supporter patrons!

### Current

- Adam Albright
- Adam P Shield
- Alexander Roper
- Andrei Sebastian Cîmpean
- Anton Smyk
- Arman Imani
- Björn Fahller
- Clint Rajaniemi
- Corentin Gay
- David C Black
- Dennis Börm
- Fedor Alekseev
- Florian Sommer
- Gwendolyn Hunt
- Jack Glass
- Jaewon Jung
- Jeff Bakst
- Kacper Kołodziej
- Lars Ove Larsen
- Magnus Westin
- Martin Hammerchmidt
- Matt Godbolt
- Matthew Guidry
