# CHAPTER 15

# Enumerated Types and Bit Flags

+   In this chapter:
Enumerated Types ................................................................ 361
Bit Flags ................................................................................ 367
Adding Methods to Enumerated Types ...................................... 371

In this chapter, I'll discuss enumerated types and bit flags. Because Windows and many programming languages have used these constructs for so years, I'm sure that many of you are already familiar with how to use enumerated types and bit flags. The common language runtime (CLR) and the Framework Class Library (FCL) work together to make enumerated types and bit flags object-oriented types that offer features that I must inspect most developers aren't familiar with. It's amazing to me how these features, which are the focus of this chapter, make developing code so much easier.

# Enumerated Types

An enumerated type is a type that defines a set of symbolic name and value pairs. For example, the Color type shown here defines a set of symbols, with each symbol identifying a single color.

```
internal enum Color {
    White // Assigned a value of 0
    Red // Assigned a value of 1
    Green // Assigned a value of 2
    Blue // Assigned a value of 3
    Orange // Assigned a value of 4
}
```

Of course, programmers can always write a program using 0 to represent white, 1 to represent red, and so on. Why use an enumerated type instead, for at least two reasons:

+   Enumerated types make the program much easier to write, read, and maintain. With enumerated types, the symbolic name is used throughout the code, and the programmer doesn't have to mentally map the meaning of each hard-coded value (for example, where white is 0 or vice versa). Also, should a symbol's numeric value change, the code can be recompiled without requiring any changes to the source code. In addition, documentation tools and other utilities, such as a debugger, can show meaningful symbolic names to the programmer.