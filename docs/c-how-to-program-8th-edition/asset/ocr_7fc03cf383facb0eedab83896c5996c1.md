attending a C++ Standards Committee meeting. The paper suggested a website where C++ programmers could find and share libraries and foster further C++ development. That idea eventually developed into the Boost Library at www.boost.org. Boost has grown to over 100 libraries, with more being added frequently. Today there are thousands of programmers in the Boost community.

# *Adding a New Library to Boost*

Boost accepts useful, well-designed, portable libraries from anyone willing to contribute. Potential Boost libraries should conform to the C++ Standard and use the C++ Standard Library—or other appropriate Boost libraries. There is a formal acceptance process to ensure that libraries meet Boost’s high quality and portability standards.

The community’s interest in a library is determined by posting to mailing lists and reading the responses. If there is interest in a library, a preliminary submission of the library is posted in the [Boost Sandbox](svn.boost.org/svn/boost/sandbox/)—a code repository for libraries that are under development. The Sandbox allows other users to experiment with the library and provide feedback.

When the library is ready for a formal review, the code submission is posted to the Sandbox Vault and a review manager is selected from a list of approved volunteers. The review manager makes sure the code is ready for formal review, sets up the review schedule, reads all user reviews, and makes the final decision whether or not to accept the library. The review manager may accept the library with certain corrections or improvements that must be implemented before the library is officially added to Boost. Once a library has been accepted, the author is responsible for its maintenance.

# *The Boost Software License*

The Boost Software License (www.boost.org/users/license.html) grants the rights to copy, modify, use and distribute the Boost source code and binaries for any commercial or noncommercial use. The only requirement is that the copyright and license information be distributed with any source code that is made public, though it isn’t required that the source code be released. These conditions allow the Boost libraries to be used in any application. Every Boost library must conform to these conditions.

# *Installing the Boost Libraries*

The Boost libraries can be used with minimal setup on many platforms and compilers. BoostPro Computing offers a free installer for using Boost with Visual Studio at www.boostpro.com/download. Most Linux distributions offer packages for Boost, though it is sometimes split up into separate packages for the headers and libraries. An installation guide available at www.boost.org/more/getting_started/index.html provides setup instructions for many compilers and platforms.

# 23.4  Boost Libraries Overview

There are many Boost libraries—too many to cover in this book. In this section, we overview some of the most useful and popular libraries. The ones listed here are part of the next C++ standard—C++0x. In the following sections, we demonstrate two of these libraries as implemented by using their implementations from the C++0x standard library.