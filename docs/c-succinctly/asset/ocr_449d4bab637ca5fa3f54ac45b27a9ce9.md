# # Chapter 9 Strings

# ## Introduction

Strings are one of those troublesome things in C and C++. In the early days of the languages, strings were all character arrays, typically 7-bit ASCII (though perhaps EBCDIC on IBM mainframes that C was ported to). Then came a mess of OS-specific workarounds, such as code pages, to allow for languages with characters that were not in the English alphabet. After a period of chaos, came Unicode. Then Unicode. And then Unicode again. And a few more Unicodes here and there as well, which is the root of the problem today.

Unicode is, in essence, two things. It’s a defined series of code points in which there is a one-to-one mapping of a particular code point to a particular value, some are graphic, others control and manipulate formatting or other required information. Everyone who uses Unicode agrees on all of these, including the private-use code points, which all agree are reserved for Unicode-conforming applications. So far, so good.

Then there are the encoding schemes where the divisions come from. There are 1,114,112 code points in Unicode. How do you represent them? The answer was the encoding schemes. UTF-16 was the first. It was later followed by UTF-8 and UTF-32. There are also endianess issues with some of these.

Other formats came and went, some of which were never even part of Unicode.

Windows ultimately adopted UTF-16 as did .NET and Java. Many GNU/Linux and other UNIX-like systems adopted UTF-8. Some UNIX-like systems use UTF-32. Some might use UTF-16. The web uses UTF-8 for the most part, due to that encoding’s intentional design to be mostly backward compatible with ASCII. As long as you are working on one system, all is well. When you try to become cross-platform, things can become more confusing.

# ## `char*` Strings

The `char*` strings (pointers to arrays of char) originally meant ASCII strings. Now they *sometimes* mean ASCII, but more frequently, they mean UTF-8. This is especially true in the UNIX world.

When programming for Windows, generally, you should assume that a `char*` string is an ASCII string or a code-page string. Code pages use the extra bit left over from 7-bit ASCII to add another 128 characters, thus creating a lot of localized text still fitting within one byte per character.

# ## `wchar_t*` Strings

`wchar_t*` strings (pointers to arrays of wchar_t, also called *wide characters*) use a different, implementation-dependent character set. On Windows, this means a 16-bit value, which is used for UTF-16. You should always work with `wchar_t` as your native character type for Windows unless you have to support really, really old OS versions (i.e., the old Windows 9X series).

When you write a wide character string constant in code, you prefix the opening double quotes with an L. For example: `const wchar_t* s = L"Hello World";`. If you only need a single character, you again use the `L`, but with single quotes: `wchar_t ch = L'A';`.

# ## `std::string` and `std::wstring` Strings

The `std::string` and `std::wstring` classes are found in the `<string>` header file. As you might imagine, `std::string` corresponds to `char*` while `std::wstring` corresponds to `wchar_t*`.