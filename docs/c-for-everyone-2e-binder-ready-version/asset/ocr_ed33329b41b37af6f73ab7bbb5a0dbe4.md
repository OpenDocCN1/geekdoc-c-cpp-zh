+   - `left, right`  
+     Manipulator: Left- or right-justifies values if they are shorter than the field width.
+   - `scientific`  
+     Manipulator: Selects scientific floating-point format, such as 1.729000e+03.
+   - `setfill(char c)`  
+     Manipulator: Sets the fill character to the character c.
+   - `setprecision(int n)`  
+     Manipulator: Sets the precision of floating-point values to n digits after the decimal point in fixed and scientific formats.
+   - `setw(int n)`  
+     Manipulator: Sets the width of the next field.

# ## `<iostream>`

# ### Class istream

+   - `bool istream::fail() const`  
+     Function: True if input has failed.
+   - `istream& istream::get(char& c)`  
+     Function: Gets the next character and places it into c.
+   - `istream& istream::unget()`  
+     Function: Puts the last character read back into the stream, to be read again in the next input operation; only one character can be put back at a time.
+   - `istream& istream::seekg(long p)`  
+     Function: Moves the get position to position p.
+   - `long istream::tellg()`  
+     Function: Returns the get position.

# ### Class ostream

+   - `ostream& ostream::seekp(long p)`  
+     Function: Moves the put position to position p.
+   - `long ostream::tellp()`  
+     Function: Returns the put position.

# ## `<fstream>`

# ### Class ifstream

+   - `void ifstream::open(const char n[])`  
+     Function: Opens a file with name n for reading.

# ### Class ofstream

+   - `void ofstream::open(const char n[])`  
+     Function: Opens a file with name n for writing.