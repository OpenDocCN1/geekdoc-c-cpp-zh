```
53  boost::sregex_token_iterator tokenIterator( testString2.begin(),
54      testString2.end(), boost::regex(",\\s"), -1 ); // token iterator
55  boost::sregex_token_iterator end; // empty iterator
56
57  while ( tokenIterator != end ) // tokenIterator isn't empty
58  {
59      output += "\"" + *tokenIterator + "\", "; // add the token to output
60      tokenIterator++; // advance the iterator
61  } // end while
62
63  // delete the ", " at the end of output string
64  cout << output.substr( 0, output.length() - 2 ) << "]" << endl;
65
66  return 0;
67 } // end of function main
```

Original string: This sentence ends in 5 stars *****
^ substituted for *: This sentence ends in 5 stars ^^^^^
"carets" substituted for "stars": This sentence ends in 5 carets ^^^^^
Every word replaced by "word": word word word word word word ^^^^^

Original string: 1, 2, 3, 4, 5, 6, 7, 8
Replace first 3 digits by "digit": digit, digit, digit, 4, 5, 6, 7, 8
string split at commas ["1", "2", "3", "4", "5", "6", "7", "8"]

# Fig. 21.5 | Using regex_replace algorithm. (Part 2 of 2.)

"stars" in testString1 with the string "carets". Lines 33–34 use regex_replace to replace every word in testString1 with the string "word".

Lines 41–45 replace the first three instances of a digit ("\d") in testString2 with the text "digit". We pass an additional argument, boost::format_first_only, to regex_replace (lines 43–44). This argument tells regex_replace to replace only the first substring that matches the regular expression. Normally regex_replace would replace all occurrences of the pattern. We put this call inside a for loop that runs three times; each time replacing the first instance of a digit with the text "digit". We use a copy of testString2 (line 39) so we can use the original testString2 for the next part of the example.

Next we use a regex_token_iterator to divide a string into several substrings. A regex_token_iterator iterates through the parts of a string that match a regular expression. Lines 53 and 55 use sregex_token_iterator, which is a typedef that indicates the results are to be manipulated with a string::const_iterator. We create the iterator (lines 53–54) by passing the constructor two iterators (testString2.begin() and testString2.end()), which represent the beginning and end of the string to iterate over and the regular expression to look for. In our case we want to iterate over the parts of the string that don't match the regular expression. To do that we pass -1 to the constructor. This indicates that it should iterate over each substring that doesn't match the regular expression. The original string is broken at delimiters that match the specified regular expression. We use a while statement (lines 57–61) to add each substring to the output string (line 17). The regex_token_iterator end (line 55) is an empty iterator. We've iterated over the entire string when tokenIterator equals end (line 57).