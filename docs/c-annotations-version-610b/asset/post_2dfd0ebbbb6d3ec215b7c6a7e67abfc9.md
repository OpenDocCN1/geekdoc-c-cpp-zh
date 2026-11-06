
## 5.2. A std::string Reference

- `string::iterator begin():`

  an iterator referring to the first character of the current string object is returned. With const string objects a const_iterator is returned.

- `size_type capacity() const:`

  the number of characters that can currently be stored in the string object without needing to resize it is returned.

- `int compare(string const &argument) const:`

  the text stored in the current string object and the text stored in argument is compared using a lexicographical comparison using the ASCII character collating sequence. zero is returned if the two strings have identical contents, a negative value is returned if the text in the current object should be ordered before the text in argument; a positive value is returned if the text in the current object should be ordered beyond the text in argument.

- `int compare(size_t opos, size_t on, string const &argument) const:`

  a substring of the text stored in the current string object is compared to the text stored in argument. At most on characters starting at offset opos are compared to the text in argument.

- `int compare(size_t opos, size_t on, string const &argument, size_type apos, size_type an) const:`

  a substring of the text stored in the current string object is compared to a substring of the text stored in argument. At most on characters of the current string object, starting at offset opos, are compared to at most an characters of argument, starting at offset apos. In this case argument *must* be a string object.

- `int compare(size_t opos, size_t on, char const *argument, size_t an):`

  a substring of the text stored in the current string object is compared to a substring of the text stored in argument. At most on characters of the current string object starting at offset opos are compared to at most an characters of argument. Argument must have at least an characters. The characters may have arbitrary values: the ASCII-Z value has no special meaning.

- `size_t copy(char *argument, size_t on, size_type opos) const:`

  the contents of the current string object are (partially) copied into argument. The actual number of characters copied is returned. The second argument, specifying the number of characters to copy from the current string object, is required. No ASCII-Z is appended to the copied string but can be appended to the copied text using an idiom like the following:

  ```cpp
  argument[object.copy(argument, string::npos)] = 0;
  ```

  Of course, the programmer should make sure that argument's size is large enough to accommodate the additional 0-byte.

- `char const *c_str() const:`

  the contents of the current string object are returned as an ASCII-Z terminated C-string.

- `char const *data() const:`

  the raw contents of the current string object are returned. Since this member does not return an ASCII-Z terminated C string (as c_str does), it can be used to retrieve any kind of information stored inside the current string object including, e.g., series of 0-bytes:

  ```cpp
  string s(2, 0);
  cout << static_cast<int>(s.data()[1]) << '\n';
  ```

- `bool empty() const:`

  `true` is returned if the current string object contains no data.

- `string::iterator end():`

  An iterator referring to the position just beyond the last character of the current string object is returned. With `const` string objects a `const_iterator` is returned.

- `string &erase(size_type opos, size_type on):`

  A (sub)string of the information stored in the current string object is erased.

- `string::iterator erase(string::iterator begin, string::iterator end):`

  The parameter end is optional. If omitted the value returned by the current object’s end member is used. The characters defined by the begin and end iterators are erased. The iterator begin is returned, which is then referring to the position immediately following the last erased character.

- `size_t find(string const &argument, size_type opos) const:`

  The first index in the current string object where argument is found is returned.

- `size_t find(char const *argument, size_type opos, size_type an) const:`

  The first index in the current string object where argument is found is returned. When all three arguments are specified the first argument must be a `char const *`.

- `size_t find(char ch, size_type opos) const:`

  The first index in the current string object where ch is found is returned.

- `size_t find_first_of(string const &argument, size_type opos) const:`

  The first index in the current string object where any character in argument is found is returned.

- `size_type find_first_of(char const *argument, size_type opos, size_type an) const:`

  The first index in the current string object where any character in argument is found is returned. If opos is provided it refers to the first index in the current string object where the search for argument should start. If omitted, the string object is scanned completely. If an is provided it indicates the number of characters of the `char const *` argument that should be used in the search. It defines a substring starting at the beginning of argument. If omitted, all of argument’s characters are used.

- `size_type find_first_of(char ch, size_type opos) const:`

  The first index in the current string object where character ch is found is returned.

- `size_t find_first_not_of(char ch, size_type opos) const:`

  The first index in the current string object where another character than ch is found is returned.

- `size_t find_last_of(string const &argument, size_type opos) const:`

  The last index in the current string object where any character in argument is found is returned.

- `size_type find_last_of(char const *argument, size_type opos, size_type an) const:`

  The last index in the current string object where any character in argument is found is returned. If opos is provided it refers to the last index in the current string object where the search for argument should start. If omitted, the string object is scanned completely. If an is provided it indicates the number of characters of the `char const *` argument that should be used in the search. It defines a substring starting at the beginning of argument. If omitted, all of argument’s characters are used.

- `size_type find_last_of(char ch, size_type opos) const:`

  the last index in the current string object where character ch is found is returned.

- `size_t find_last_not_of(string const &argument, size_type opos) const:`

  the last index in the current string object where any character not appearing in argument is found is returned.

- `istream &std::getline(istream &istr, string &object, char delimiter = '\n'):`

  Note: this is not a member function of the class string.

  A line of text is read from istr. All characters until delimiter (or the end of the stream, whichever comes first) are read from istr and are stored in object. If the delimiter is encountered it is removed from the stream, but is not stored in object.

  If the delimiter is not found, istr.eof returns true (see section 6.3.1). Since streams may be interpreted as bool values (cf. section 6.3.1) a commonly encountered idiom to read all lines from a stream successively into a string object line looks like this:

  ```cpp
  while (getline(istr, line))
      process(line);
  ```

  The contents of the last line, whether or not it was terminated by a delimiter, are eventually also assigned to object.

- `string &insert(size_t opos, string const &argument, size_type apos, size_type an):`

  a (sub)string of argument is inserted into the current string object at the current string object's index position opos. Arguments for apos and an must either both be provided or they must both be omitted.

- `string &insert(size_t opos, char const *argument, size_type an):`

  argument (of type char const *) is inserted at index opos into the current string object.

- `string &insert(size_t opos, size_t count, char ch):`

  Count characters ch are inserted at index opos into the current string object.

- `string::iterator insert(string::iterator begin, char ch):`

  the character ch is inserted at the current object's position referred to by begin. Begin is returned.

- `string::iterator insert(string::iterator begin, size_t count, char ch):`

  Count characters ch are inserted at the current object's position referred to by begin. Begin is returned.

- `string::iterator insert(string::iterator begin, InputIterator abegin, InputIterator aend):`

  the characters in the range defined by the InputIterators abegin and aend are inserted at the current object's position referred to by begin. Begin is returned.

- `size_t length() const:`

  the number of characters stored in the current string object is returned.

- `size_t max_size() const:`

  the maximum number of characters that can be stored in the current string object is returned.
