
Output from your program should be sent to the terminal window (your screen) as well as the requested `csis.txt` output file. Be sure to read the document on Capturing Program Output. Your full name and Palomar ID number must appear as a comment in the source file that contains `main()`. Be sure to include the `csis.txt` output file in your zip archive.

Be sure to do error checking when attempting to open a file for input or output. For extra credit, pass all file names to this lab as `command-line arguments`. Compiler specific information regarding command-line arguments can be found in Blackboard at this location:

## Docs | Set Command-Line Arguments

The contents of `getty.txt` is given below:

> Four score and seven years ago our fathers brought forth, upon this continent, a new nation, conceived in liberty, and dedicated to the proposition that all men are created equal. Now we are engaged in a great civil war, testing whether that nation, or any nation, so conceived, and so dedicated, can long endure. We are met here on a great battlefield of that war. We have come to dedicate a portion of it as a final resting place for those who here gave their lives that that nation might live. It is altogether fitting and proper that we should do this. But in a larger sense we can not dedicate – we can not consecrate – we can not hallow this ground. The brave men, living and dead, who struggled here, have consecrated it far above our poor power to add or detract. The world will little note, nor long remember, what we say here, but can never forget what they did here. It is for us, the living, rather to be dedicated here to the unfinished work which they have, thus far, so nobly carried on. It is rather for us to be here dedicated to the great task remaining before us that from these honored dead we take increased devotion to that cause for which they here gave the last full measure of devotion – that we here highly resolve that these dead shall not have died in vain; that this nation shall have a new birth of freedom; and that this government of the people, by the people, for the people, shall not perish from the earth.

For more practice with command-line arguments, write a program, grep.c, which searches a file, or a group of files, for a pattern and outputs each line of the file that contains an instance of the pattern. Your program should prefix the filename to each line that matches, so you can tell in which file the match takes place.

The syntax for the grep command is:

```
grep [option] pattern file(s)
```

where option consists of one or more single characters preceded by a hyphen, pattern consists of the text to search for, and file(s) tells grep which file or files to search.

The following options should be recognized:

- **-v Non-match:** Only non-matching lines are printed. Only lines that do not contain the search string are considered to be non-matching lines.
- **-i Ignore case:** grep ignores upper/lowercase differences. grep treats all letters a-z as being identical to the corresponding letters A-Z in all situations.
- **-n Numbers:** Each matching line that grep prints is preceded by its relative line number in the file.
- **-c Count only:** Only a count of matching lines is printed. For each file that contains at least one matching line, grep prints the file name and a count of the number of matching lines. Matching lines are not printed.
- **-l List match files:** Only the name of each file containing a match is printed. After grep finds a match, it prints the filename and processing immediately moves on to the next file.

Note that matches will not cross line boundaries (i.e., a match must be contained on a single line). Be sure to include appropriate error checking routines in case the requested files do not exist.

Using the three files shown below, show the output generated for each of the following commands:

```
grep the genesis.txt
grep the getty.txt genesis.txt shakes.txt
grep hello getty.txt genesis.txt shakes.txt
grep the genesis.txt foo.txt shakes.txt
grep -v the getty.txt
grep -l and shakes.txt
grep -n the genesis.txt shakes.txt
grep -c the getty.txt shakes.txt genesis.txt
grep -l in getty.txt shakes.txt genesis.txt
```

Here are the contents of each of the files:

## getty.txt

Four score and seven years ago our fathers brought forth, upon this continent, a new nation, conceived in liberty, and dedicated to the proposition that all men are created equal.

## shakes.txt

All the world's a stage,
And all the men and women merely players.
They have their exits and their entrances;
And one man in his time plays many parts.

## genesis.txt

In the beginning God created the heaven and the earth. Now the earth was uniform and void, and darkness was upon the face of the earth and the spirit of God hovered over the face of the waters. And God said: 'Let there be light.' And there was light. And God saw the light, that it was good: and God divided the light from the darkness. And God called the light day, and the morning He called night. And there was evening and there was morning, one day.

For extra credit, see if you can generalize your program so that it works with more than one option at a time.

Remember that the `main()` function should appear as the first function in the program. Be sure to use function prototypes for each of the functions that are used in your program.

Output from your program should be sent to the terminal window (your screen) as well as the requested `csis.txt` output file. Be sure to read the document on Capturing Program Output. Your full name and Palomar ID number must appear as a comment in the source file that contains `main()`. Be sure to include the `csis.txt` output file in your zip archive.

## Text Encryption Lab

### Part 1

The Computer Science Program here at Palomar College has recently developed a NetNews reader for the campus wide bulletin board system. However, one part of the reader still needs to be completed. It is necessary to include an encryption scheme that uses simple substitution to allow private communications.

The encryption scheme is known as ROT13 because it "rotates" each alphabetic character half-way around the alphabet ('a' becomes 'n', 'b' becomes 'o', 'o', 'n' becomes 'a', and so forth). Case is maintained. All white space, punctuation, numbers, etc., remain the same.

Write a program that takes an arbitrary amount of text from standard input, applies the ROT13 transformation, and write it to standard output. No input or output line will exceed 80 characters.

- Sample input: This is 1 line to be rotated.
- Guvf vf 1 yvar gb or ebbgnqrq.
- Sample output: Guvf vf 1 yvar gb or ebbgnqrq.
- This is 1 line to be rotated.

### Part 2

Write a program that asks the user to input a string password of arbitrary length. Then encode the password in the following way. Alternate placement of the vowels ('a', 'e', 'i', 'o', 'u') so that the first vowel is moved to the front of the password, the second is moved to the rear, the third to the front, the fourth to the rear, etc. Encoding should stop when the last character of the input string has been examined. Print out the encoded password.

- Sample input: computer science
- olympiad
- Sample output: eeocmptr scnuie
- aolympdi

Output from your program should be sent to the terminal window (your screen) as well as the requested `csis.txt` output file. Be sure to read the document on Capturing Program Output. Your full name and Palomar ID number must appear as a comment in the source file that contains `main()`. Be sure to include the `csis.txt` output file in your zip archive.

Storage Class

Storage Location

- Storage Class Homework

## Storage Class

Every variable in C has two attributes, _storage type_ and _storage class_. Storage type determines the meaning of values. Storage class determines storage location, lifetime and visibility or scope (region where a variable may be referenced.) There are four storage classes: _automatic (local)_, _external_, _register_ and _static_.

### Automatic Variables

Automatic or local variables are the most common type of storage class. Variables declared within function bodies are, by default, automatic or local. These variables are known only within the function in which they are declared. As far as any other function is concerned, they don't exist.

Local variables are recreated each time the function is called and values from the previous calls will not be retained. Local variables may be given values in their declarations:

```
void foo(void) {
    int num = 5;
}
```

Note that automatic or local variables may be declared not only at the start of a function, but also at the start of a block:

```
// storage1.c

void foo(void) {
    char x;
    int num;
    ...
    if (num > 5) {
        int x;
        for (x = 0; x < num; x++) {
        ...
        }
    }
}
