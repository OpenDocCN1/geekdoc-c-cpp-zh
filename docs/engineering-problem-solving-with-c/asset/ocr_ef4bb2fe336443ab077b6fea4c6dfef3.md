# Decomposition Outline

+   1. Read a character from the file.
+   2. Determine if character is part of an html tag.
+   3. Print all characters that are not part of an html tag.

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
```