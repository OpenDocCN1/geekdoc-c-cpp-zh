```
outStream.setf(ios::showpoint);
outStream.precision(2);
```

To explain this magic formula, we will consider the instructions in reverse order.

Every output stream has a member function named precision. When your program executes a call to precision such as the previous one for the stream outStream, then from that point on in your program, any number with a decimal point that is output to that stream will be written with a total of two significant figures, or with two digits after the decimal point, depending on when your compiler was written. The following is some possible output from a compiler that sets two significant digits:

```
23.      2.2e7    2.2      6.9e-1    0.00069
```

The following is some possible output from a compiler that sets two digits after the decimal point:

```
23.56    2.26e7    2.21     0.69     0.69e-4
```

In this book, we assume the compiler sets two digits after the decimal point.

A call to precision applies only to the stream named in the call. If your program has another output stream named outStreamTwo, then the call to outStream.precision affects the output to the stream outStream but has no effect on the stream outStreamTwo. Of course, you can also call precision with the stream outStreamTwo; you can even specify a different number of digits for the numbers output to the stream outStreamTwo, as in the following:

```
outStreamTwo.precision(3);
```

The other formatting instructions in our magic formula are a bit more complicated than the member function precision. We now discuss these other instructions. The following are two calls to the member function setf with the stream outStream as the calling object:

```
outStream.setf(ios::fixed);
outStream.setf(ios::showpoint);
```

setf is an abbreviation for set flags. A flag is an instruction to do something in one of two possible ways. If a flag is given as an argument to setf, then the flag tells the computer to write output to that stream in some specific way. What it causes the stream to do depends on the flag.

In the previous example, there are two calls to the function setf, and these two calls set the two flags ios::fixed and ios::showpoint. The flag ios::fixed causes the stream to output numbers of type double in what is called fixed-point notation, which is a fancy phrase for the way we normally write numbers. If the flag ios::fixed is set (by a call to setf), then all floating-point numbers (such as numbers of type double) that are output to that stream will be written in ordinary everyday notation, rather than e-notation.