There are three ways of splitting strings in Objective-C. The first is obvious: Simply iterate over the characters until you find a convenient place for a split and then use -substringWithRange: to create the new token. This will work in the general case, but is quite a lot of effort for something that should be trivial.

In C, you can use the strsep() function, or the deprecated strtok() function, to split a string anywhere that a character in a specific set is found. The -componentsSeparatedByCharactersInSet: method on NSString works in almost exactly the same way, although it takes anCharacters as an argument instead of a string.

You can make this method behave like strtok_r() by constructing a character set using +characterSetWithCharactersInString:. The NSString method returns an NSArray with the substrings. This works exactly like the C functions; you get empty strings wherever there are two adjacent separator characters.

Alternatively, you can split a string based on occurrences of a specific substring. This is very useful when you have separators composed of several characters.