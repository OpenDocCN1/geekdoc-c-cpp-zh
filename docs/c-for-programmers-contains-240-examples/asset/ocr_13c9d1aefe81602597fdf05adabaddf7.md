```
```cpp
105    return sPtr[ subscript ]; // non-const return; modifiable lvalue
106 } // end function operator[]
107
108 // return reference to character in String as rvalue
109 char String::operator[]( int subscript ) const
110 {
111     // test for subscript out of range
112     if ( subscript < 0 || subscript >= length )
113     {
114         cerr << "Error: Subscript " << subscript
115              << " out of range" << endl;
116         exit 1); // terminate program
117     } // end if
118
119     return sPtr[ subscript ]; // returns copy of this element
120 } // end function operator[]
121
122 // return a substring beginning at index and of length subLength
123 String String::operator()( int index, int subLength ) const
124 {
125     // if index is out of range or substring length < 0,
126     // return an empty String object
127     if ( index < 0 || index >= length || subLength < 0 )
128         return ""; // converted to a String object automatically
129
130     // determine length of substring
131     int len;
132
133     if ( ( subLength == 0 ) || ( index + subLength > length ) )
134         len = length - index;
135     else
136         len = subLength;
137
138     // allocate temporary array for substring and
139     // terminating null character
140     char *tempPtr = new char[ len + 1 ];
141
142     // copy substring into char array and terminate string
143     strncpy( tempPtr, &sPtr[ index ], len );
144     tempPtr[ len ] = '\0';
145
146     // create temporary String object containing the substring
147     String tempString( tempPtr );
148     delete [] tempPtr; // delete temporary array
149     return tempString; // return copy of the temporary String
150 } // end function operator()
151
152 // return string length
153 int String::getLength() const
154 {
155     return length;
156 } // end function getLength
```
```

**Fig. 11.10** | String class member-function and friend-function definitions. (Part 3 of 4.)