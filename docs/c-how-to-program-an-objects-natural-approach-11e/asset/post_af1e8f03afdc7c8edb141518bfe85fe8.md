
- OpenML focuses on open-source tools and data for machine learning.
- OpenAI researches artificial intelligence and publishes open-source tools used in AI research. They’re also the creators of ChatGPT and DALL-E 2, which have each generated enormous interest in artificial intelligence. See Section 1.16 for more about these technologies.
- OpenCV focuses on open-source computer-vision tools that can be used across various operating systems and programming languages.
- The Python Software Foundation is responsible for the Python programming language.
- The Boost organization manages the development of the open-source Boost C++ libraries (see Section 1.7).

Rapid improvements to computing and communications, decreasing costs and open-source software have made it much easier and more economical to create software-based businesses now than just a decade ago. A great example is Facebook, which was launched from a college dorm room and built with open-source software.

The Linux kernel is the core of the most popular open-source, freely distributed, full-featured operating system. It’s developed by a loosely organized team of volunteers and is popular in servers, personal computers and embedded systems (such as the computer systems at the heart of smartphones, smart TVs and automobile systems). Unlike Microsoft’s Windows and Apple’s macOS source code, the Linux source code is available to the public for examination and modification, and is free to download and install. As a result, Linux users benefit from a massive community of developers actively debugging and improving the kernel, and the ability to customize the operating system to meet specific needs.

## Apple’s macOS and Apple’s iOS for iPhone® and iPad® Devices

Apple, founded in 1976 by Steve Jobs and Steve Wozniak, quickly became a leader in personal computing. In 1979, Jobs and several Apple employees visited Xerox PARC (Palo Alto Research Center) to learn about Xerox’s desktop computer that featured a graphical user interface (GUI). That GUI served as the inspiration for the Apple Macintosh, launched in 1984.

The Objective-C programming language, created by Stepstone in the early 1980s, added object-oriented programming (OOP) capabilities to the C programming language. Steve Jobs left Apple in 1985 and founded NeXT Inc. In 1988, NeXT licensed Objective-C from Stepstone. NeXT developed an Objective-C compiler and libraries, which were used as the platform for the NeXTSTEP operating system’s user interface and Interface Builder (for constructing graphical user interfaces).

Jobs returned to Apple in 1996 when they bought NeXT. Apple’s macOS operating system is a descendant of NeXTSTEP. Apple has several other proprietary operating systems derived from macOS:

- iOS is used in iPhones.
- iPadOS is used in iPads.
- watchOS is used in Apple Watches.
- tvOS is used in Apple TV devices.

- **2. (True/False)** Proprietary code is often scrutinized by a much larger audience than open-source software, so errors often get removed faster.  
  **Answer:** False. Open-source code is often scrutinized by a much larger audience than proprietary software, so errors often get removed faster.

## 1.6 C and C++

### C Programming Language

C was implemented in 1972 by Dennis Ritchie at Bell Laboratories. It initially became widely known as the UNIX operating system’s development language. Today, most of the code for general-purpose operating systems is written in C or C++. C is available for most computers and is hardware independent. With careful design, it’s possible to write C programs that are portable to most computers.

The widespread use of C with various kinds of computers (sometimes called hardware platforms) led to many variations. The American National Standards Institute (ANSI) cooperated with the International Organization for Standardization (ISO) to standardize C worldwide—the joint standard document was published in 1990. An updated standard is currently under development.

### C++ Programming Language

C++^44^ was developed by Bjarne Stroustrup in 1979 at Bell Laboratories as an extension of C. Originally called “C with Classes,” it was renamed C++ in the early 1980s—the name derives from C’s increment operator, ++, which adds 1 to a number. It provides many features that “spruce up” C, but more importantly, it includes capabilities for object-oriented programming inspired by the Simula simulation programming language. As you’ll see, C++ has evolved over the last 40 years to enable programmers to use five different programming models, each of which you’ll learn in this book:

- procedural programming,
- object-oriented programming,
- functional-style programming,
- generic programming, and
- template metaprogramming.

**C++ is the premier language for building high-performance, business-critical and mission-critical computing systems**, including operating systems, real-time systems, embedded systems, game systems, banking systems, air-traffic-control systems, communications systems and more. Even for systems programmed primarily in other languages, C++ is often used to build the performance-intensive portions of those systems. Stroustrup maintains a lengthy list of C++ applications on his website at

https://www.stroustrup.com/applications.html

^44^ Stroustrup, Bjarne. “A History of C++: 1979–1991.” Accessed March 18, 2023. https://www.stroustrup.com/holm12.pdf.

### Modern C++

Today's C++ programmers build systems and system components using Modern C++, which includes the C++20, C++17, C++14 and C++11 standards—the digits in each name indicate the year in the 2000s when that version was approved by the ISO C++ standard committee. Many of the language and library features introduced by these standards make C++ easier to use, improve runtime performance and software quality, and enable applications to take advantage of today’s multi-core systems.

C++ is over four decades old, so there is much existing C++ code using older programming idioms—this is typically referred to as legacy code. We emphasize Modern C++ idioms in this book.

### C++ Core Guidelines

Bjarne Stroustrup, Herb Sutter (the ISO C++ committee chair) and several other contributors^45^ created the evolving C++ Core Guidelines,^46^ containing extensive recommendations and sample code to help you use Modern C++ correctly and effectively. Various code-analysis tools (discussed in Preface Section 7) enable you to check your code to ensure it follows these recommendations. We cite the C++ Core Guidelines frequently throughout this book.

### ✓ Checkpoint

- **1. (Fill-In)** Most code for general-purpose operating systems is written in __________.  
  **Answer:** C or C++.
- **2. (Fill-In)** The __________ provide recommendations and sample code to help you use Modern C++ correctly and effectively.  
  **Answer:** C++ Core Guidelines.

## 1.7 C++ Standard Library and Open-Source Libraries

C++ programs consist of pieces called functions and classes. You can program all the pieces you’ll need yourself. Instead, most C++ programmers reuse the rich collections of classes and functions in the C++ standard library. Thus, there are really two parts to learning C++ programming:

- learning the C++ language itself (often referred to as the “core language”), and
- learning how to use the C++ standard library’s classes and functions.

### The Boost Project and Other Open Source Libraries

There are enormous numbers of open-source C++ libraries that can help you perform significant tasks by writing only modest amounts of code. The Boost C++ libraries provide 168 powerful open-source libraries.^47^ Boost serves as a “breeding ground” for new capabilities.

^45^ “C++ Core Guidelines—Acknowledgments.” Accessed March 18, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#SS-ack.

^46^ “C++ Core Guidelines.” Accessed March 18, 2023. https://isocpp.github.io/CppCoreGuidelines/

^47^ “Boost 1.81.0 Library Documentation.” Accessed March 18, 2023. https://www.boost.org/doc/libs/1_81_0/.
