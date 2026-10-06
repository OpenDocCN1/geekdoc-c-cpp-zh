
# Text Files 249

While this code is easy, it is also inefficient, particularly in the cases where n is prime. The reason is that we do not need to go up to n-1. If there is no divisor less than the square root of n, it cannot be one. If n were very large, the difference between n and the square root of n would be significant. A more efficient function can be written in this way.

```
def isPrime(n:Long):Boolean = {
  var i = 2
  while (i<=n && n%i!=0) i += 1
}
```

A Range type could have been used with a square root function, but the math.sqrt function works with Doubles that introduces difficulties we did not want to deal with. You might wonder about the use of a while loop here. After all, we generally prefer the for loop. In this case, the while loop only allows us an easy way to check if anything that divides into is the square root of n. On the other hand, a for loop runs for every member of a collection. The forall method-the-method used above is simple enough to break out early as well. There are more efficient ways of determining if a number is prime. You do not need to check all the values up to the square root of n. You only need to check the numbers up to that point. We leave it as an exercise to the reader to determine how you might write code that would use that approach to more efficiently determine if a number is prime across many calls to the function.

# 9.6 End of Chapter Material

## 9.6.1 Summary of Concepts

- Files are important to real applications as values stored in memory are lost when a program terminates. Files allow data to persist between runs. They can also be used as a source of large data sets.
- Minimal file interactions can be accomplished with I/O redirection. This approach comes with significant limitations for interactive programs.
- Large groups of code, like the libraries for Scala and Java, have to be broken into pieces. Packages are groups of code that have common functionality.
- Names that include full package specifications can be very long. import statements can be used to allow the programmer to use shorter names.
- One way to read files is using scala.io.Source.

- A call to Source.fromFile will return an instance of BufferedSource that pulls data from the file.
- Source is an Iterator[Char]. The Iterator part implies that it is a collection that is consumed as values are pulled off. It gives individual characters.
- The getLines method returns an Iterator[String] with elements that are full lines.

# 250 Introduction to Programming and Problem-Solving Using Scala

- The split method on String is useful for breaking up lines into its constituent parts. It takes a delimiter as a String and returns an Array[String] of all the parts of the String that are separated by that delimiter.
- You can use the Source.URL(url:String) method to get a Source that can read data from a source on the web in the format of a URL.
- For applications it is easier to read data from a java.util.Scanner. This does not provide a Scala style collection, but it has methods for checking if types of values are present and reading them in a way that is more independent of line breaks.
- You can use the java.io.PrintWriter to write text data to file. This type has print methods like those that you have already familiar with.

# 9.6.2 Self-Directed Study

Enter the following statements in the REPL and see what they do. Some will produce errors. You should try to figure out why. Try some variations to make you understand what is going on.

# 9.6.3 Exercises

1. If you did project 6.7, you can modify it so that it does not have to use input redirection. Make a function that reads in the dictionary of words and then write a script that will allow the user to input Scrabble letters until they enter a special value to stop.

2. Create a file with the letters of the alphabet on one line separated by spaces. The challenge is that you cannot manually type in a String with that.

3. Create a file with the letters of the alphabet with one letter on each line.

4. Write scripts that copy a file using each of the following constructs. They should take two command line arguments for the input file name and the output file name.
    - while loop
    - for loop
    - Higher order methods
    - Recursion
    - You can repeat each of the above using getLines if you did not the first time or without it you used it the first time.

5. Write scripts using each of the different methods from exercise 4 that capitalizes every letter.

6. Write scripts using each of the different methods from exercise 4 that shift each vowel up. So, "a" becomes "e" and so forth.

7. Write a script that takes a number of rows and columns as command-line arguments and outputs a file with a matrix of random numbers of size.

8. Write a script that takes a filename as a command-line argument and reads in a matrix of numbers that form file. It should print out the row and column sums and averages. This poem is less scary by substituting a parrot (or some other bird of your choice) for the raven and then output the newly revised poem to a file. A text file for this poem can be found at: http://www.textfiles.com/etext/AUTHORS/POE/raven-702.txt.

10. Go to http://www.gutenberg.org/files/3201/files/, find the text you could play with. The text file that we need for this exercise is CROSSWD.TXT. Write a program that counts the number of words that do not have an "e" in them and counts each word.

# 9.4 Projects

1. There is a utility in Linux called wc which stands for "word count". You can run it on one or more files, and it will tell you how many lines, words, and characters are there in the files. For projects you will do the same, only you should count how many times each letter occurs in each file (regardless of case). The files you should work on will be specified on the command line. Your program should read through each file and count how many characters, words, and lines are as well as how many times each letter occurs. You will print this information for each file followed by a grand total for all the files. Your program may be invoked by scala wc.scala *.txt, which would go through all the ".txt" files in the current directory.

You will consider any string that is between white spaces to a word. To make the counting of letters easier doing this: "abcdef".map(c=> c-'a') to see what it does and think about how that can help you.

# Introduction to Programming and Problem-Solving Using Scala

Back in section 9.5 we went through a few simple forms of encryption. This might keep people from reading your files, but you would not want to make changes to your bank account using them. The encryption techniques we use for sending sensitive messages rely heavily on number theory. The most common systems today are all called public-key cryptography. In this type of system, each user has some information that they make, the public-key, and some they keep, the private-key. For this project, you will implement a simple version of the RSA cryptosystem.

The way the RSA cryptosystem works is the following:

(a) Select two prime numbers $p$ and $q$ such that $p \neq q$. The level of security of the system depends on how big $p$ and $q$ are. For good security you want them to be 512-1024 bits, far larger than what can store in an Int or a Long. Finding large primes.
(b) Compute $n = pq$.
(c) Select an odd integer $e$, that is relatively prime to $(p-1)(q-1)$.
(d) Compute $d$, the multiplicative inverse of $e$, modulo $(p-1)(q-1)$. The technique for finding this is described in exercise 8.10.
(e) The pair $(e, n)$ is the RSA-public. You or anyone who wants to see these values then
(f) The pair $(d, n)$ is the private-key. You need this to decode a message and do not want anyone else to have it.
(g) To encode a message, $M$, the sender $P(M) = M^e \mod n$. For this to work you need to break the message into chunks that can be encoded into numbers, $M$, that are less than $n$.
(h) To decode the message use $S(C) = C^d \mod n$, where $C$ is the encrypted message you got from the sender.

3. The proper to represent a recipe is using a file. The same thing is true for the contents of your pantry. For this project you will extend project 8.10 to include options for building a cookbook with file access for the pantry. The script should take two command-line arguments for a pantry file and a recipe file. These files should be loaded when the program starts. The menu should have the following options:

    - (a) Add a pantry item.
    - (b) Print pantry contents.
    - (c) Add a recipe.
    - (d) Check a recipe.
    - (e) Cook recipe.
    - (f) Quit

When the user selects "Quit" option. The files should be written to reflect new changes. You simply have to make the code that writes it with the code that it reads.

In this version, the "Add recipe" option should have the user type in a unique name of a recipe followed by item names and. That should be remembered so that the "Check recipe" option allows the user to type in just a name.
