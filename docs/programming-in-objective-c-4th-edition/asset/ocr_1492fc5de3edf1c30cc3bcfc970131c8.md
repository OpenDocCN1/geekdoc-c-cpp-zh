```
NSLog("@str1 == str2");
else // must be NSOrderedDescending
NSLog("@str1 > str2");

// Convert a string to uppercase

res = [str1 uppercaseString];
NSLog("@Uppercase conversion: %s", [res UTF8String]);

// Convert a string to lowercase

res = [str1 lowercaseString];
NSLog("@Lowercase conversion: %@", res);

NSLog("@Original string: %@", str1);
}
return 0;
```

# Program 15.3. Output

Length of str1: 16
Copy: This is string A
Concatenation: This is string AThis is string B
str1 == res
str1 < str2
Uppercase conversion: THIS IS STRING A
Lowercase conversion: this is string a
Original string: This is string A