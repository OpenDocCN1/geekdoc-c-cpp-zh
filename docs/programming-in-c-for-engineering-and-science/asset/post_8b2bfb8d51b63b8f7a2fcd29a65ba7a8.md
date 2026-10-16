
indicating that the plus operator + was specified, and not ++ or +=. The y is left in the stream where it can be subsequently processed in the normal fashion the next time the compiler asks the lexical analyzer for a token.

An alternative to peek() is to use get() to retrieve the next character,

```
inStream.get(nextCh);
```

and then use putback() to return it to inStream, if necessary:

```
if (nextCh == '=')
{
    inStream.get(nextCh);
    return PLUS_EQUALS_TOKEN;
}
else if (nextCh == '+')
{
    inStream.get(nextCh);
    return INCREMENT_TOKEN;
}
else if (isspace(nextCh) || isalnum(nextCh) || nextCh == '\'' || nextCh == '\"')
{
    inStream.putback(nextCh);
    return PLUS_TOKEN;
}
else
{
    // ... generate error message
}
// illegal token
```

Thus, if the value of nextCh were 'y', putback(nextCh) would return that character to the stream so that it will be accessed the next time the compiler asks the lexical analyzer for a token.

We've seen how the clear() function can be used to reset the status bits of a stream to their default values. Sometimes, however, it is useful to be able to set them to specified values, and this can be done using the setstate() function.

To illustrate, suppose that we have a problem involving five types of beam design: I-beam, C-channel, flitch, cantilever, and hip, and we want to write a readBeam() function to input a beam design, similar to the getline() function provided by the string library. Our function will read a word from a stream into a string variable, which it then passes back to the caller via a reference parameter.

But what do we do if the user enters an invalid value, a word that is not one of the five beam designs? To handle this situation in a way that is consistent with the iostream library, our function should set the fail status bit for that input stream. Example 11.4 shows how the stream function member setstate() can be used to do this.

### Example 11.4 Setting Stream-Status Flags

```
void readBeam(istream & theStream, string & beam)
{
    string beamType;
    theStream >> beamType;

    if (beamType == "I-beam" || beamType == "C-channel" ||
        beamType == "flitch" || beamType == "cantilever" ||
        beamType == "hip")
        beam = beamType;
    else
    {
        theStream.seekg(-beamType.size(), ios::cur);    // unread the word
        theStream.setstate(ios::failbit);            // indicate failure
    }
}
```

By setting the fail status bit in the stream, this function leaves the handling of the error up to its caller. For example, a programmer wishing to treat this as a fatal error can write

```
string aBeamType;
readBeam(cin, aBeamType);
assert( cin.good() );
```

and if the user enters any word other than one of the five beam designs, the call to assert() will terminate the program. By contrast, a programmer who wishes to treat this occurrence as a nonfatal error and have the user try again, can write

```
string aBeamType;
for (;;)
{
    readBeam(cin, aBeamType);
    if ( cin.good() ) break;
    cout << "Try again: ";
    cin.clear();
    cin.ignore(80, '\n');
}
```

and the user will be given more chances to enter a valid value. Such flexibility is a trademark of good design, because it leaves the decision of how to handle the problem up to users of the function, allowing them to choose the approach they prefer.

The setstate() function can be used to set the status bits in a stream, which are referred to by the following names:

| Status Bit | Description |
|---|---|
| `ios::badbit` | The bad bit: 1 if an unrecoverable error occurred, 0 otherwise. |
| `ios::failbit` | The fail bit: 1 if a recoverable error occurred, 0 otherwise. |
| `ios::eofbit` | The eof bit: 1 if the end-of-file mark was read, 0 otherwise. |

In practice, setstate() is rarely passed ios::eofbit, because that is set by the input operations.

### 11.3.3.1 The Formatting Manipulators

As we saw in Chapter 7, the iostream and iomanip libraries provide manipulators for controlling the format of output streams. Manipulators can be divided into two categories: those without arguments and those that require arguments.

Format manipulators that do not require arguments are available in the iostream library. Some of the basic ones are given in the following table:

| Manipulator | Description |
|---|---|
| `boolalpha` | Use strings `false` and `true` for I/O of boolean values |
| `noboolalpha` | Use integers 0 and 1 for I/O of boolean values |
| `scientific` | Use floating-point (scientific) notation |
| `fixed` | Use fixed-point notation |
| `showpoint` | Show decimal point and trailing zeros for whole real numbers |
| `noshowpoint` | Hide decimal point and trailing zeros for whole real numbers |
| `showpos` | Display positive values with a + sign |
| `noshowpos` | Display positive values without a + sign |
| `dec` | Display integer values in base 10 |
| `oct` | Display integer values in base 8 |
| `hex` | Display integer values in base 16 |
| `showbase` | Display integer values indicating their base (e.g., `0x` for hex) |
| `noshowbase` | Display integer values without indicating their base |
| `uppercase` | In hexadecimal, use symbols A–F; in scientific, use E |
| `nouppercase` | In hexadecimal, use symbols a–f; in scientific, use e |
| `skipws` | Skip white space on input |
| `noskipws` | Don't skip white space on input |
| `flush` | Write contents of stream to screen (or file) |
| `endl` | Insert newline character and flush the stream |
| `left` | Left-justify displayed values, pad with fill character on right |
| `right` | Right-justify displayed values (except strings), pad with fill character on left |
| `internal` | Pad with fill character between sign or base and value |

As we saw in Chapter 7, manipulators are inserted into the stream, but instead of appending values to the stream (except for endl), they affect the format of values inserted subsequently into the stream. For example, if we were to write

```
int i = 17;

cout << showbase
    << oct << i << endl
    << dec << i << endl
    << hex << i << endl;
```

then the following values would be displayed

```
021
17
0x11
```

To use the manipulators that require arguments, the iomanip library must be included. The table below gives some of these manipulators.

| Manipulator | Description |
|---|---|
| `setprecision(num)` | Set the number of decimal digits to be displayed to `num` |
| `setw(num)` | Display the next value in a field whose width is `num` |
| `setfill(ch)` | Set the fill character to `ch` (blank is the default) |

When a real number is inserted into a stream, the number of digits that are displayed to the right of the decimal point is called the precision of the number. As we have seen before, this characteristic can be controlled with the setprecision() manipulator.

We have also seen that when a number is inserted into a stream, it is first placed into a field, which is then inserted into the stream. The size of this field is controlled by the setw() manipulator. If the size of the field is less than the size of the value being displayed, the field is automatically expanded to the same size as the value. If the size of the field exceeds the size of the value being displayed, then the empty positions in the field are filled with the fill character (by default, a blank), whose value is set by the setfill() manipulator.

Here is a simple code fragment that illustrates the use of these manipulators:

```
cout << fixed << showpoint        // show decimal pt, sign
    << setprecision(2)             // 2 decimal places
    << setfill('*') << left         // pad with *, left justify
    << setw(6) << 1.0/3.0 << endl   // print value
    << setfill('$') << right        // pad with $, right justify
    << setw(6) << 1.0/3.0 << endl;
```

When executed, this statement produces the following output:

```
0.33**
$$0.33
```

Note that unlike setprecision(), setw() affects only the next value inserted into the stream, so setw() must precede each insertion of a value whose field width we wish to specify.

To display a column of figures with their decimal points aligned, the right manipulator can be used with setprecision() and setw(). For example, to display a table of square roots to seven decimal places, we could write this code segment:

```
cout << fixed << showpoint << right
    << setprecision(7);
for (int i = 1; i <= 10; i++)
    cout << setfill(' ') << setw(2) << i
        << setfill('.') << setw(12) << sqrt(i) << endl;
```

Executing these statements produces the output

```
1...1.0000000
2...1.4142136
3...1.7320508
4...2.0000000
5...2.2360680
6...2.4494897
7...2.6457513
8...2.8284271
9...3.0000000
10...3.1622777
```

### 11.3.4 String Streams

C++ also permits us to read input from a string or to write output to a string. This is made possible by means of string streams defined in the sstream library:[10]

| `istringstream` | For input from a string |
| `ostringstream` | For output to a string |
| `stringstream` | For input from and output to a string |

The str() function can be used to convert a string stream to a string, and vice versa:

| `strstream.str(s);` | Set string stream `strstream` to a copy of string `s` |
| `strstream.str()` | Returns a string that is a copy of the string in `strstream` |

[10] The corresponding types for wide characters (of type wchar_t) are wistringstream, wostringstream, and wstringstream.
