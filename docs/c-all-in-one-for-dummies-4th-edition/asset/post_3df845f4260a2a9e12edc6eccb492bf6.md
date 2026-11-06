
![](img/128ab511de4e7360e167e3b15cdd5dd0_832_0.png)

**FIGURE 3-4:** Add new files using the New from Template dialog box.

![](img/128ab511de4e7360e167e3b15cdd5dd0_832_1.png)

**FIGURE 3-5:** Define the header requirements.

## Coding the library

At this point, you have what amounts to a blank header file in a static library project. Your static library could conflict with other libraries, so it’s important to add a namespace to your code. The example uses `MyNamespace`, but normally you’d use something related to you as a person or your company, such as `MyCompanyInc`. The MathLibrary header, in Listing 3-5, shows what you need to create the library used for this example.

**LISTING 3-5: Creating a Static Library**

```cpp
#ifndef MATHLIBRARY_H_INCLUDED
#define MATHLIBRARY_H_INCLUDED

#include <iostream>
#include <cmath>

using namespace std;

namespace MyNamespace {
    template<typename T> T Area(T height, T length) {
        return height * length;
    }

    const double PI = 4.0*atan(1.0);
    template<typename T> T CircleArea(T radius) {
        double result;
        result = PI * radius * radius;
        // This version truncates the value.
        return (T)result;
    }

    template<typename T> T TriangleArea(T base, T height) {
        double result;
        result = base * height * 0.5;
        return (T)result;
    }
}

#endif // MATHLIBRARY_H_INCLUDED
```

As you can see, this is a portable form of the math library discussed in the “Creating a Basic Math Template” section, earlier in this chapter. Of course, the library form has changes. You have the usual `#define` statements and the use of a namespace to encapsulate all the code. Notice that the namespace comes after all the declarations.

**In This Chapter**

- Considering what Boost can do for you
- Getting, installing, and building Boost
- Working with the various Boost tools
- Integrating and using the Boost documentation
- Creating your first application using Boost

## Chapter 4 Investigating Boost

As your skill with C++ improves, you find that you need additional functionality that doesn’t come with the Standard Library. For example, the simple act of checking a string for specific character sequences (such as a telephone number pattern) can prove difficult. You can do it, but most developers will think that someone else has certainly crossed this bridge before. The answer to the question of where to find the additional code you need is third-party libraries. One of the most popular C++ libraries is Boost, which is the topic of this chapter and the next.

Two book chapters can’t serve as a complete reference to an entire library — especially not a set of libraries the size of Boost. This particular chapter (Chapter 4) has a set of more limited goals. It introduces you to Boost and helps you understand why Boost may be helpful to your development efforts. It also shows you how to obtain and install Boost, demonstrates some Boost tools, and finally helps you create your first application using Boost. Chapter 5 picks up where this chapter leaves off and helps you use Boost to build some interesting applications. In short, these two chapters combined provide you with an overview of a library that you should consider spending more time discovering.

Standard Library (rather than the other way around). Check out the site at https://caiorss.github.io/C-Cpp-Notes/boost-libraries.html as well, because it’s more complete than most sources. When thinking about these moves, C++11 uses these Boost features, among many others:

- `std::regex`
- `std::tuple`
- `std::function`
- Threading
- Smart pointers

Each version of C++ with its associated Standard Library comes with new additions. When you move to C++17, you see these additions from Boost (along with many others):

- Vocabulary types: `std::variant`, `std::any`, and `std::optional`
- `string_view`
- Searchers: Boyer-Moore and Boyer-Moore-Horspool
- `std::filesystem`
- Special math functions
- Template enhancements

The main point here is that Boost is a proving ground, while the Standard Library tends to act as a repository for tested functionality. If your goal is to build stable applications that use tested techniques, Boost may not be the solution you’re looking for. However, when you need to implement the latest C++ features, you really need to use Boost.

### Defining the trade-offs of using the Standard Library

As mentioned in the previous section, the Standard Library tends toward using stable techniques. You therefore don’t necessarily find the best solution to a problem in the Standard Library if C++ is deficient in an area at the outset. However, you need to consider the transitional phase of an application, where it can move from using Boost to the Standard Library. Consider these sites that provide

![](img/128ab511de4e7360e167e3b15cdd5dd0_838_0.png)

![](img/128ab511de4e7360e167e3b15cdd5dd0_838_1.png)

that they won’t pay anything for using Boost, even in a commercial setting. In addition, Boost doesn’t have any expenses, so you probably won’t ever need to pay for it. You need to download Boost 1.73 (the version used for this book) from the https://www.boost.org/users/history/version_1_73_0.html site before proceeding with the rest of this chapter (you see installation instructions later in the chapter after the explanation of Boost features). You should probably read the associated Getting Started guide (the index page is at https://www.boost.org/doc/libs/1_73_0/more/getting_started/index.html) so that you know how to perform the installation for your platform. A number of people and organizations contribute to Boost. You can check out their pictures at https://www.boost.org/users/people.html.

![](img/128ab511de4e7360e167e3b15cdd5dd0_840_0.png)

However, don’t get the idea that Boost is completely free. If you want commercial-level support, you’ll pay for it, just as you would with any other product. Only the library itself is free. The following sections describe some of the details of Boost.

### Boost features

You might think that Boost couldn’t really be all that complete if you can get it for free. Actually, Boost includes a significant number of features — far more features than the average developer will use in writing typical applications. It’s interesting to note that you probably have an application on your system that relies on Boost: Adobe Acrobat. That’s right; major applications do rely on Boost because it’s a feature-rich application development library. In fact, you can see entire lists of applications you know and use at https://www.boost.org/users.html (simply choose one of the categories, such as Shrink-Wrapped Boost, to see the applications in that category).

The current version of Boost contains in excess of a hundred libraries in categories that meet an incredible number of needs (new libraries are added all the time). You can see a list of these libraries at https://www.boost.org/doc/libs/1_73_0/. In some cases, you’ll need only Boost to meet all your development needs. Because these libraries meet specific conformity requirements, you never find yourself calling a function one way with one library and another way when using a different library.

![](img/128ab511de4e7360e167e3b15cdd5dd0_840_1.png)

In addition to libraries, Boost also provides a number of tools to make your development experience more enjoyable. Most of this chapter discusses these specialized tools. Because you get the source code for all the tools, you can build a version of the tool for every platform in your organization, which means that every developer can use the same toolset. Using a common toolset reduces training time and tends to improve the consistency of development output.

![](img/128ab511de4e7360e167e3b15cdd5dd0_840_2.png)
