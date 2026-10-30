Encoding and decoding support is provided by the Osp::Text namespace classes, while Osp::Base classes provide the underlying support for native Unicode, including the mchar wide-character data type wchar_t.

> Note: mchar is supported at compiler level as a native type by the Sourcery G++ GNU Toolchain, which is used for target and simulator builds in the bada SDK. Be aware that for the sake of efficiency, the bada mchar type is defined with a 2-byte size, that is, 16-bits. On most GNU-based platforms, mchar is defined with a 4-byte size. Therefore any code that depends on the physical size of an mchar will not behave correctly if ported to bada without change. Of course, programming best practice would say that code should not depend on the physical size of a data type.

And by the way, bada also provides excellent support for localisation generally, and not just for writing language. Support includes date, time, and time zones, number, currency, and other locale-sensitive information types, including conversions and formatting, as well as IDE support for string resources.

# 4.3.3 Using Buffers

Just as strings should always be used instead of native C-style null-terminated character arrays (because strings are inherently Unicode, and size-checking means that they cannot overflow), the Buffer class is preferred to native, C-style arrays.

Buffers are container classes that wrap arrays (sequences) of C++ primitive types, for example int, long, double, and char. (Compare with strings – which are sequences of non-primitive type, Character.) Buffers provide absolute and relative indexing, as well as a mark that stores an index:

+   - ByteBuffer is a wrapper class for sequences of 8-bit unsigned int.
+   - BufferType is provided to enable ready-made template classes of double, float, int, long, longlong, mchar, and short primitive types.

> Note: A DoubleBuffer is a Buffer double object, not to be confused with the ‘double buffering’ buffer management technique!

# 4.3.4 Collection Classes

An essential ingredient of any well-designed class library is a good set of collection classes. In keeping with its minimalist design philosophy (it’s a language for