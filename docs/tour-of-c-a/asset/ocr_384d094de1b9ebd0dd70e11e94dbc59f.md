[17] Use manipulators or format(t) to control formatting; §11.6.1, §11.6.2.

[18] precision(t) specifications apply to all following floating-point output operations; §11.6.1.

[19] Floating-point specifications (e.g., scientific) apply to all following floating-point output operations; §11.6.1.

[20] Include <ios> or <iostream> when using standard manipulators; §11.6.

[21] Stream formatting manipululators are "sticky" for use for many values in a stream; §11.6.1.

[22] Include <iomanip> when using standard manipulators taking arguments; §11.6.

[23] We can output time, dates, etc. in standard formats; §11.6.1, §11.6.2.

[24] Don't try to copy a stream: streams are move only; §11.7.

[25] Remember to check that a file stream is attached to a file before using it; §11.7.2.

[26] Use stringstreams or memory streams for in-memory formatting; §11.7.3; §11.7.4.

[27] We can define conversions between any two types that both have string representation; §11.7.3.

[28] C-style I/O is not type-safe; §11.8.

[29] Unless you use printf-family functions call ios_base::sync_with_stdio(false); §11.8; [CG: SL.io.10].

[30] Prefer <filesystem> to use direct of platform-specific interfaces; §11.9.