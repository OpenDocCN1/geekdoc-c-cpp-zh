```
cout << std::dec val << endl; // Output: 255
cout << std::hex val << endl; // Output: 0xff
f();
cout << std::oct << val << endl; // Output: 0377
cout << val << std::endl; // Output: 0377
}
```

# Listing 27.6 Number formats for std::showbase manipulator in output.

First, I use the std::showbase manipulator so that the number base 0x for hexadecimal or o for octal values appears. I could have skipped the manipulator dec at this point because it is the default setting, and thus the value is output in decimal form anyway.

Next is the hex manipulator, which causes the value to be output in hexadecimal notation. The setting remains global for the stream, as confirmed by the output of the f() function. Then the value is output in octal representation after applying the oct manipulator. The very last output shows again that the setting remains for the stream. If you want to have the decimal notation again, you must reset the format with the dec manipulator.

# Manipulators for Floating-Point Numbers

There are also some manipulators (floatfield flags) for floating-point numbers, which are also included in <ios> and listed in Table 27.4.

| Manipulator | Meaning |
| --- | --- |
| fixed | Output in floating-point notation: 3.14159. |