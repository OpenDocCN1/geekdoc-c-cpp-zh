```
12  char sentence[] = "This is a sentence with 7 tokens";
13  char *tokenPtr;
14
15  cout << "The string to be tokenized is:\n" << sentence
16      << "\n\nThe tokens are:\n\n";
17
18  // begin tokenization of sentence
19  tokenPtr = strtok( sentence, " " );
20
21  // continue tokenizing sentence until tokenPtr becomes NULL
22  while ( tokenPtr != NULL )
23  {
24      cout << tokenPtr << '\n';
25      tokenPtr = strtok( NULL, " " ); // get next token
26  } // end while
27
28  cout << "\nAfter strtok, sentence = " << sentence << endl;
29  return 0; // indicates successful termination
30  } // end main
```

The string to be tokenized is:
This is a sentence with 7 tokens

The tokens are:

This
is
a
sentence
with
7
tokens

After strtok, sentence = This

Fig. 8.33 | Using strtok to tokenize a string. (Part 2 of 2.)

Subsequent calls to strtok to continue tokenizing sentence contain NULL as the first argument (line 25). The NULL argument indicates that the call to strtok should continue tokenizing from the location in sentence saved by the last call to strtok. Note that strtok maintains this saved information in a manner that is not visible to you. If no tokens remain when strtok is called, strtok returns NULL. The program of Fig. 8.33 uses strtok to tokenize the string "This is a sentence with 7 tokens". The program prints each token on a separate line. Line 28 outputs sentence after tokenization. Note that strtok modifies the input string; therefore, a copy of the string should be made if the program requires the original after the calls to strtok. When sentence is output after tokenization, note that only the word "This" prints, because strtok replaced each blank in sentence with a null character ('\0') during the tokenization process.

> Common Programming Error 8.22
> 
> Not realizing that strtok modifies the string being tokenized, then attempting to use that string as if it were the original unmodified string is a logic error.