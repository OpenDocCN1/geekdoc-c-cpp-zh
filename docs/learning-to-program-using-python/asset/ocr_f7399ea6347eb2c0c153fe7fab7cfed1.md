+   – If sep is not specified or is None, a different splitting algorithm is applied: runs of consecutive whitespace are regarded as a single separator, and the result will contain no empty strings at the start or end if the string has leading or trailing whitespace. Consequently, splitting an empty string or a string consisting of just whitespace with a None separator returns [].

+   – For example, '1 2 3'.split() returns ['1', '2', '3'], and '1 2 3'.split(None, 1) returns ['1', '2 3']. str.splitlines([keeplines]) Return a list of the lines in the string, breaking at line boundaries. Line breaks are not included in the resulting list unless keepends is given and true.

**str.startswith**(*prefix*[,* start*, *end*])

+   – Return True if string starts with the prefix, otherwise return False. prefix can also be a tuple of prefixes to look for. With optional start, test string beginning at that position. With optional end, stop comparing string at that position.

**str.strip**([*chars*])

+   – Return a copy of the string with the leading and trailing characters removed. The chars argument is a string specifying the set of characters to be removed. If omitted or None, the chars argument defaults to removing whitespace. The chars argument is not a prefix or suffix; rather, all combinations of its values are stripped.

**str.swapcase**()

+   – Return a copy of the string with uppercase characters converted to lowercase and vice versa.

**str.title**()

+   – Return a titlecased version of the string: words start with uppercase characters, all remaining cased characters are lowercase. There is also a method to determine if a string is a title **istitle**().