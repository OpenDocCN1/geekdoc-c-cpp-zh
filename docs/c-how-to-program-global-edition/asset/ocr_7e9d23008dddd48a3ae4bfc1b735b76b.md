![](bbox=[0.12, 0.07, 0.88, 0.28])

Fig. 8.26 | Using function strtok. (Part 2 of 2.)

Multiple calls to strtok are required to tokenize a string—i.e., break it into tokens (assuming that the string contains more than one token). The first call to strtok (line 15) contains two arguments: a string to be tokenized, and a string containing characters that separate the tokens. In line 15, the statement

```
char * tokenPtr = strtok(string, " "); // begin tokenizing sentence
```

assigns tokenPtr a pointer to the first token in string. The second argument, " ", indicates that tokens are separated by spaces. Function strtok searches for the first character in string that's not a delimiting character (space). This begins the first token. The function then finds the next delimiting character in the string and replaces it with a null ('\0') character to terminate the current token. Function strtok saves a pointer to the next character following the token in string and returns a pointer to the current token.

Subsequent strtok calls in line 20 continue tokenizing string. These calls contain NULL as their first argument. The NULL argument indicates that the call to strtok should continue tokenizing from the location in string saved by the last call to strtok. If no tokens remain when strtok is called, strtok returns NULL. You can change the delimiter string in each new call to strtok. Figure 8.26 uses strtok to tokenize the string "This is a sentence with 7 tokens". Each token is printed separately. Function strtok modifies the input string by placing '\0' at the end of each token; therefore, a copy of the string should be made if the string will be used after the calls to strtok. [Note: Also see CERT recommendation STR06-C, which discusses the problems with assuming that strtok does not modify the string in its first argument.]

# 8.9 Memory Functions of the String-Handling Library

The string-handling library functions presented in this section manipulate, compare and search blocks of memory. The functions treat blocks of memory as character arrays and can manipulate any block of data. Figure 8.27 summarizes the memory functions of the string-handling library. [Note: Each of these functions has a more secure version described in optional Annex K of the C11 standard. We mention these in the Secure C Programming section of this chapter.]

The pointer parameters are declared void * so they can be used to manipulate memory for any data type. Recall from Chapter 7 that any pointer can be assigned directly to a pointer of type void *, and a pointer of type void * can be assigned directly to a pointer of any other type. Because a void * pointer cannot be dereferenced, each function receives a size argument that specifies the number of bytes the function will process. For