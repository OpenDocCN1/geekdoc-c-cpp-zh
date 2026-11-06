+   - `int ios::width(int nchars);`

the field width of the next insertion operation is set to `nchars`, returning the previously used field width. This setting is not persistent. It is reset to 0 after every insertion operation. Manipulator: `std::setw(int)`. Example:

```
cout.width(5);
cout << 12;                 // using 5 chars field width
cout << setw(12) << "hello";  // using 12 chars field width
```

# 6.3.2  Formatting flags

Most formatting flags are related to outputting information. Information can be written to output streams in basically two ways: using binary output information is written directly to an output stream, without converting it first to some human-readable format and using formatted output by which values stored in the computer’s memory are converted to human-readable text first. Formatting flags are used to define the way this conversion takes place. In this section all formatting flags are covered. Formatting flags may be (un)set using member functions, but often manipulators having the same effect may also be used. For each of the flags it is shown how they can be controlled by a member function or if available- a manipulator.

# **To display information in wide fields:**

+   - `ios::internal:`

to add fill characters (blanks by default) between the minus sign of negative numbers and the value itself. Other values and data types are right-adjusted. Manipulator: `std::internal`. Example:

```
cout.setf(ios::internal, ios::adjustfield);
cout << internal;        // same, using the manipulator

cout << '\/' << setw(5) << 5 << "\n";  // displays '    5'
```

+   - `ios::left:`

to left-adjust values in fields that are wider than needed to display the values. Manipulator: `std::left`. Example:

```
cout.setf(ios::left, ios::adjustfield);
cout << left;             // same, using the manipulator

cout << '\/' << setw(5) << "hi" << "\n";  // displays 'hi   '
```

+   - `ios::right:`

to right-adjust values in fields that are wider than needed to display the values. Manipulator: `std::right`. This is the default. Example:

```
cout.setf(ios::right, ios::adjustfield);
cout << right;            // same, using the manipulator

cout << '\/' << setw(5) << "hi" << "\n";  // displays '  hi'
```

# **Using various number representations:**

+   - `ios::dec:`

to display integral values as decimal numbers. Manipulator: `std::dec`. This is the default. Example:

```
cout.setf(ios::dec, ios::basefield);
cout << dec;             // same, using the manipulator
cout << 0x10;            // displays 16
```