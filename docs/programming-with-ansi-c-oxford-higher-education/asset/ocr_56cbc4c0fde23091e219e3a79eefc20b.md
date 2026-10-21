there would have been a need to ensure that the programmer does not name the functions the same as those in the C++ standard library itself (or some other third-party library, which is already installed in the target machine). The identifier names of the programmer now have no chance of collision with the standard library identifier names.

# 12.4 PREDEFINED AND WIDE CHARACTER STREAMS

C++ has a few predefined streams. Whenever a C++ program starts execution, these streams automatically open on their own. Table 12.1 lists the predefined streams.

| Stream | Meaning | Default source/destination |
|--------|---------|---------------------------|
| cin | Standard input stream | Keyboard |
| cout | Standard output stream | Screen |
| cerr | Standard error stream with no buffer | Screen |
| clog | Standard error stream with buffer | Screen |

To receive an international standardization from the International Organization for Standardization (ISO), the designers of C++ have added some specific features to enable to work globally. One each such feature is the support for wide character streams. Some of the languages (e.g., Chinese) cannot accommodate themselves in the small 8-bit footprint of ANSI. They require bigger 16-bit Unicode to represent their character set. These streams are win, wout, werr, and wlog.

# 12.5 C++ STREAMS CLASSES HIERARCHY

![](bbox=[0.05, 0.57, 0.95, 0.82])

The I/O hierarchy shown in Fig. 12.1 is usually mentioned without the prefix basic_, that is, basic_ios is usually referred to as ios. The ios_base class contains the details not needed for templatization. basic_ios and its descendants are all templatized. basic_streambuf provides the mechanism to access the stream using lower-level functions. It also provides services to other classes. There are a few more items in the hierarchy that are not mentioned here. One can refer to Stroustrup's classic The C++ Programming Language for further details.

# 12.6 FORMATTED AND UNFORMATTED I/O

We have already studied about unformatted I/O using cout. The operator << is usually used with cout object to support unformatted output. Though not used much, there are other ways of formatting I/O. Later on, we will see how rich formatting is possible using operator <<. Besides the default << operator, there are other ways to provide unformatted I/O.