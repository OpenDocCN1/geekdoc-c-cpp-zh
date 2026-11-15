
![](img/0235a4ea835dc4575bd036e024a533b3_239_0.png)

## 3. HAND EXAMPLE

For the hand example, we will use a very small html file that just has a few lines. Here is the sample html file:

```
<HTML>
<HEAD>
<META HTTP-EQUIV="Content-Type" CONTENT="text/html;
charset=ISO-8859-1">
<TITLE>HomePage</TITLE>
<META NAME="GENERATOR" CONTENT="Internet Assistant for
Microsoft Word 2.04z">
</HEAD>
<BODY BGCOLOR = "#118187" >
<HR>
<><Font size=4>
<P>
J. Ingber
<br>
Accurate Solutions in Applied Physics, LLC
<br>
Albuquerque, New Mexico
</b></<Font>
</BODY>
</HTML>
```

The text without tags should be

HomePage
J. Ingber
Accurate Solutions in Applied Physics, LLC
Albuquerque, New Mexico

## 4. ALGORITHM DEVELOPMENT

We first develop the decomposition outline because it breaks the solution into a series of sequential steps.

### Decomposition Outline

- 1. Read a character from the file.
- 2. Determine if character is part of an html tag.
- 3. Print all characters that are not part of an html tag.

The first step in the decomposition outline involves a loop in which we read each character from the file. The condition to exit the loop will be a test for the end of the file. Our program will have two distinct states. In one state, we will be reading the text of the file (not a tag), so we will output each character as we read it. In the other state, we will be reading a tag, so the character will not be printed. We will use an object of type `bool` to keep track of which state we are in. If we are in the text state, the character `<` will mark the beginning of a tag. If we are in the tag state, the character `>` will mark the end of a tag. The refinement in pseudocode is as follows:

```
Refinement in Pseudocode
main: set text_state to true
read character
while not end-of-file
if text_state is true
if character = '<'
set text_state to false
else
print character to file
else
if character = '>'
set text_state to true
read next character
```

The steps in the pseudocode are now detailed enough to convert into C++:

```
/*-----------------------------------------------------------*/
/* Program chapter5_6 */
/* This program reads an html file, and writes the text */
/* without the tags to a new file. */
/*-----------------------------------------------------------*/
#include<iostream> //Required for cin, cout, cerr.
#include<fstream> //Required for ifstream, ofstream.
#include<string> //Required for string.
using namespace std;
int main()
{
// Declare objects.
char character;
bool text_state(TRUE);
string infile, outfile;
ifstream html;
ofstream htmltext;

// Prompt user for name of input file.
cout << "enter the name of the input file";
cin >> infile;
// Prompt user for name of output file.
cout << "enter the name of the output file";
cin >> outfile;
// Open files.
html.open(infile);
if(html.fail())
{
    cerr << "Error opening input file\n";
    exit(1);
}
htmltext.open(outfile);
// Read first character from html file.
html.get(character);
while(!html.eof())
{
// Check state.
if(text_state)
{
    if(character == '<') // Beginning of a tag,
        text_state=FALSE; // Change States.
    else
        htmltext << character; // Still text, write to
    // the file.
}
else
{
// Command state, no output required.
if(character == '>') // End of tag,
    text_state = TRUE; // Change States.
}
// Read next character from html file.
html.get(character);
}
html.close();
htmltext.close();
return 0;
}
```

## 5. TESTING

Using the html file from the hand example, we get the following output:

```
HomePage
J. Ingber
Accurate Solutions in Applied Physics, LLC
Albuquerque, New Mexico
```

This matches the output from the hand example.

### Modify 5.4

- 1. Modify program chapter5_6 by replacing the if statements with switch statements.
- 2. The pseudocode for program chapter5_6 is provided. Write the corresponding flowchart.

## 5.5 Error Checking

In the previous sections, we used the fail() function to test the state of an input stream to determine if an error had occurred while trying to open a file. Errors can also occur while attempting to read data from a file or from standard input. An input stream will be set to an error state if the input data is not what the input statement is expecting.

Consider the following statements that attempt to read two values from standard input:

```
int iVar1(0), iVar2(0);
cin >> iVar1 >> iVar2;
cout << iVar1 << " " << iVar2 << endl;
```

Since the variables ivar1 and ivar2 are declared to be of type int, the data entered from the keyboard must be two integer numbers, separated by whitespace. In C++, whitespace is defined as blank, tab, newline, formfeed, and carriage return. If any other type of data is encountered, such as a decimal point, a comma, or any nonnumeric character other than whitespace, cin will be set to an error state.

Suppose the following data were entered at the keyboard:

```
10,20
```

When the enter key is pressed at the end of the line, the data is stored in the standard input buffer. The contents of the standard input buffer and its associated pointer, after pressing the enter key, is illustrated in Figure 5.3:

```
1 0 , 2 0 \n
```

Figure 5.3 Standard input buffer.

Note that the newline character, generated by pressing the enter key, is stored as a single character in the input buffer. A trace of statements attempting to read from the input buffer is shown below.

| Statement | Memory Snapshot |
|---|---|
| `int iVar1(0), iVar2(0);` | `integer iVar1 0 integer iVar2 0` |
| `cin >> iVar1 >> iVar2;` | `integer iVar1 10 integer iVar2 0` |
| `cout << iVar1 << " " << iVar2 << endl;` | |
| **Standard Output** | `10 0` |

We can see that the characters 1 and 0 are extracted from the input buffer, converted to the integer value 10, and assigned to iVar1. Since a comma cannot be interpreted as integer data, the comma is left in the input buffer. No error occurs after the first extraction since the integer value 10 was successfully extracted and assigned to iVar1. When the >> operator attempts to extract a value for the integer variable iVar2, the comma is encountered. Since a comma is not a numeric character, it is not whitespace, the comma is left in the input buffer. No value is extracted, and thus, no value is assigned to iVar2. Since the extraction for iVar2 was unsuccessful, the value of iVar2 is unchanged and cin is now in an error state. The cout statement is executed next and the output 10 0 is displayed on the screen. The standard input buffer has been modified as illustrated in Figure 5.4.

```
, 2 0 \n
```

Figure 5.4 Standard input buffer.

![](img/0235a4ea835dc4575bd036e024a533b3_243_0.png)

When an input stream is in an error state, the program continues to execute but input operations applied to the stream will result in a null operation, which means that the input buffer will not be modified.

In order to access the input buffer and extract the value 20, we must first set cin back to an error free state. Once cin is in a good state, the comma can be extracted from the input stream and then the value 20 can be extracted and assigned to iVar2. The function clear() can be used to set cin to an error free state. We illustrate the use of the clear() function, and other functions defined in the stream class hierarchy and designed to handle stream errors, in the following section.

| Event | badbit | failbit | eofbit | goodbit |
|---|---|---|---|---|
| Initialization of a stream. | 0 | 0 | 0 | 1 |
| Failure to open a file. | 0 | 1 | 0 | 0 |
| Unexpected data encountered. | 0 | 1 | 0 | 0 |
| End of file encountered. | 0 | 1 | 1 | 0 |

### The Stream State

Every stream has an associated state. The state of a stream is represented as a set of variables defined in the class ios_base. These variables are often referred to as state flags. Recall that all classes in the stream class hierarchy inherit from ios_base. Thus, every stream has an associated set of state flags. State flags indicate a Boolean state which can be represented by a value of 0 or 1. These flags can be set and tested to handle potential errors.

The state of a stream is affected by events that occur when operations are applied to the stream, as illustrated in Table 5.1. Note that the names of the state flags include the word bit. Recall that a bit is a binary digit and can represent a value of 0 or 1. Thus, the names indicate the Boolean nature of the flags.

We see from Table 5.1 that the goodbit is initialized to true when a stream is first created and remains true as long as the eofbit, the failbit, and the badbit remain false. The eofbit is set to true when an end of file is encountered. The failbit of a stream is set to true when an attempt to open a file fails, an end-of-file is encountered, or unexpected data corrupts the input stream. The state of these bits determines the state of the associated stream.

The badbit will be set to true if the stream becomes corrupted and data is assumed to be lost. Input routines in some user-defined class types and class templates set the bad bit to true when input data does not match the required format.

The state of a stream can be tested and directly modified using functions defined within the stream class hierarchy. These functions are designed to facilitate error handling, and should be used in all programs that rely on correct input for correct results. Table 5.2 provides a partial list of functions defined within the stream class hierarchy.

| Function | Description |
|---|---|
| bool bad() | Returns true if badbit is set. |
| bool eof() | Returns true if eofbit is set. |
| bool fail() | Returns true if failbit is set. |
| bool good() | Returns true if goodbit is set. |
| void clear(iostate flag=goodbit) | Sets the state flags. |
| iostate rdstate() | Returns value of state flags. |

Program chapter5_7 illustrates the use of these functions to handle input errors.
