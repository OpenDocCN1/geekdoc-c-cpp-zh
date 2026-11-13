# REPLACE FUNCTIONS:

These functions replace len characters of s starting at s[i]. The value of i must be less than or equal to s.size( ), and if there are fewer than len characters starting at this spot, then all characters to the end of the string are replaced. The new characters are specified using one of the forms of arguments shown earlier.

+   - s.replace(i, len, str)
+   - s.replace(i, len, str, index, n)
+   - s.replace(i, len, n, c)
+   - s.replace(i, len, carray)
+   - s.replace(i, len, array, n)

# FUNCTIONS TO FIND A POSITION IN A STRING:

These functions return a value of type string::size_type. The return value is the constant string::npos if the character is not found.

+   - s.find(c) // Returns index of first occurrence of the character c in s
+   - s.find(c, i) // Returns index of first occurrence of c that is at or after s[i]
+   - s.rfind(c) // Returns index of final occurrence of the character c in s
+   - s.rfind(c, i) // Returns index of final occurrence of c that is at or before s[i]
+   - s.find(str) // Returns index of first occurrence of the substring str within s
+   - s.find(str, i) // Returns index of first occurrence of str that is at or after s[i]
+   - s.rfind(str) // Returns index of final occurrence of the substring str within s
+   - s.rfind(str, i) // Returns index of final occurrence of str that is at or before s[i]

# FUNCTIONS THAT RETURN A SUBSTRING:

+   - s.substr(i) // Returns a string containing characters from s[i] to the end of s
+   - s.substr(i, n) // Returns a string containing up to n characters, starting at s[i]

# OTHER MODIFICATION MEMBER FUNCTIONS:

+   - s.clear( ) // Removes all characters from s.
+   - s.erase( ) // Removes all characters from s.
+   - s.erase(i) // Removes all characters from s[i] to the end of s.
+   - s.erase(i, len) // Removes up to len characters starting at s[i].
+   - s.reserve(amount) // Requests that the capacity of s be changed to the specified amount (which may be smaller than the current capacity). However, the changed capacity will never be smaller than the current string size.
+   - s.resize(n, c) // Changes the length of s to n (if this increases the length, new characters are the character c).
+   - s.resize(n) // Same as s.resize(n, '\0').

# INPUT AND OUTPUT:

+   - cout << s // Print all of s to cout.
+   - cin >> s // Skip whitespace and then read characters into s until whitespace is encountered. The terminating whitespace is not read.
+   - getline(cin, s, c) // Read characters from cin into s until c is encountered. The terminating c is read but not added to the end of s.
+   - getline(cin, s) // Same as getline(cin, s, '\n')