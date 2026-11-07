# **21.5** *(True or False)* State which of the following statements are *true* and which are *false*. If a statement is false, explain why.

+   a) strings are always null terminated.
+   
+   b) Class string member function `max_size` returns the maximum size for a string.
+   
+   c) Class string member function can throw an `out_of_range` exception.
+   
+   d) Class string member function `begin` returns an iterator.

# **21.6** *(Find Code Errors)* Find any errors in the following and explain how to correct them:

```
a) std::cout << s.data() << std::endl; // s is "hello"

b) erase( s.rfind( 'x' ), 1); // s is "xenon"

c) string& foo()
   {
       string s( "Hello" );
       ...    // other statements
       return;
   } // end function foo
```

# **21.7** *(Simple Encryption)* Some information on the Internet may be encrypted with a simple algorithm known as “rot13,” which rotates each character by 13 positions in the alphabet. Thus, 'a' corresponds to 'n', and 'x' corresponds to 'k'. rot13 is an example of **symmetric key encryption**. With symmetric key encryption, both the encrypter and decrypter use the same key.

+   a) Write a program that encrypts a message using rot13.
+   
+   b) Write a program that decrypts the scrambled message using 13 as the key.
+   
+   c) After writing the programs of part (a) and part (b), briefly answer the following question: If you did not know the key for part (b), how difficult do you think it would be to break the code? What if you had access to substantial computing power (e.g., supercomputers)? In Exercise 21.4 we ask you to write a program to accomplish this.

# **21.8** *(Using string Iterators)* Write a program using iterators that demonstrates the use of functions `rbegin` and `rend`.

# **21.9** *(Words Ending in “r” or “ay”)* Write a program that reads in several strings and prints only those ending in “r” or “ay”. Only lowercase letters should be considered.

# **21.10** *(string Concatenation)* Write a program that separately inputs a first name and a last name and concatenates the two into a new string. Show the two techniques for accomplishing this task.

# **21.11** *(Hangman Game)* Write a program that plays the game of Hangman. The program should pick a word (which is either coded directly into the program or read from a text file) and display the following:

```
Guess the word:    XXXXXX
```

Each X represents a letter. The user tries to guess the letters in the word. The appropriate response yes or no should be displayed after each guess. After each incorrect guess, display the diagram with another body part filled. After seven incorrect guesses, the user should be hanged. The display should look as follows:

![](bbox=[0.233, 0.796, 0.307, 0.854])

After each guess, display all user guesses. If the user guesses the word correctly, display

> > Congratulations!!! You guessed my word. Play again? yes/no

# **21.12** *(Printing a string Backward)* Write a program that inputs a string and prints the string backward. Convert all uppercase characters to lowercase and all lowercase characters to uppercase.