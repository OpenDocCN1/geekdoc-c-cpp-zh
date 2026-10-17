# # Searching from the End of a String

If you have worked with the `index()` function, you can easily work with the `rindex()` function. The `rindex()` function differs from the `index()` function only because it begins its search from the end of the string rather than from the beginning. Using such a function at times proves an important way of increasing the efficiency of search operations. Listing04_11 provides an example of how to use the `rindex()` function.

```
```perl
#Listing04_11
#Search a string using the rindex() function

#1 Show users the string that is the target
print ("$TargetString= <<TARGET>;
Sighs for folly said and done
Twist our narrow days
TARGET

#Use the length() function
#to initialize a scalar to hold the length of the string
#Report the length
$TargetStringLength = length($TargetString);
print "\nLength of string: " . $TargetStringLength;

#2. Initialize a scalar to hold the search string
$SearchString = "";
print "\nType the string \\"fo\\" to begin a search: ";

#3. Collect input from the user
$SearchString = <STDIN>;

#4. Important! Truncate the string to eliminate the newline character
chomp($SearchString);
print "\nSearch begun for \\"" . $SearchString . "\\"...\n";

#5. Use the index function to begin the search from the end of the string
# Return the index to a scalar and report the position to the user
$IndexLocation = rindex($TargetString , $SearchString, $TargetStringLength);
print "\nString found at index " . $IndexLocation . "...\n";
```
```