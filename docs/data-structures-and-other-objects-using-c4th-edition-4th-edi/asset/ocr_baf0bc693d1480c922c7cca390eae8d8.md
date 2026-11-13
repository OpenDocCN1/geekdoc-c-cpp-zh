NULL pointer for the empty queue (otherwise list_clear does not work).

+   24. Removals will be hard to implement.
+   
+   25. If all items were kept at the front of the array, then it would be time-consuming to add or remove at the front.

+   26. For inserting at both ends, an ordinary linked list is fine; but for removing at both ends, a doubly linked list is needed.
+   
+   27. last_bp would be the third pointer on the left side of Figure 8.13.

# PROGRAMMING PROJECTS

For more in-depth projects, please see www.cs.colorado.edu/~main/projects/

+   1. In Figure 8.3 on page 399, we presented a program that checks a string to see if the letters in the string read the same forward and backward. These strings are called palindromes. Another kind of palindrome is one in which we look at words, rather than letters. A word-by-word palindrome is a string of words such that the words read the same forward and backward. For example, the quote “You can cage a swallow, can’t you, but you can’t swallow a cage, can you?” is a word-by-word palindrome. Write a program to test an input string and tell whether or not it is a word-by-word palindrome. Consider upper- and lowercase letters to be the same letter. Define a word as any string consisting of only letters or an apostrophe, and bounded at each end with one of the following: a space, a punctuation mark, the beginning of the line, or the end of the line. Your program should have a friendly interface and allow the user to check more lines until the user says he or she wishes to quit the program.

> As I was passing near the jail
> I met a man, but hurried by.
> His face was ghastly, grimly pale.
> He had a gun. I wondered why.
> He had: a Gun? I wondered...why,
> His face was ghastly! Grimly pale,
> I met a man but hurried by.
> As I was passing near the jail.

Consider upper- and lowercase versions of a letter to be the same letter. Consider word boundaries to be significant, so for example, the words in the first line must read the same as the words in the last line in order to pass the test (as opposed to just the letters reading the same); however, consider all word delimiters as being equivalent; that is, a punctuation, any number of spaces, the beginning or end of a line, or any combination of these are all considered to be equivalent. The end of the passage should be marked by a line containing only the word “end,” spelled with any combination of upper- and lowercase letters, and possibly with blanks before and/or after it. Your program should have a friendly interface and allow the user to check more passages until the user tells he or she wishes to quit the program. Note that to test your program, you don’t need to use such well-constructed poems. Your program will check any passage, regardless of its literary merit.

+   2. In Figure 8.3 on page 399, we presented a program that checks a string to see if the letters in the string read the same forward and backward. The previous exercise performed a similar check using words in place of letters. In this exercise, you are to write a program that runs a similar check using lines rather than words or letters. Write a program that reads in several lines of text and decides if the passage reads the same whether you read the lines top-to-bottom or bottom-to-top; this is yet another kind of palindrome. For example, the following poem by J. A. Lindon reads the same whether you read the lines from top to bottom or from bottom to top:

+   3. Enhance the carwash simulation procedure in Figure 8.8 on page 411 so that it has the following additional property. There is an additional parameter, which is a maximum length for the queue. When the queue gets as long as this maximum, any customer who arrives will leave without entering the queue (because she or he does not want to wait that long). There should also be one