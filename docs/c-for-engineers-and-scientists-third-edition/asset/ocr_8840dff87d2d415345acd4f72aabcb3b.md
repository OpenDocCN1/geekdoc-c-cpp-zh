# Character I/O

Although you have used cin and getline() to accept data entered from the keyboard in a more or less "cookbook" manner, you need to understand what data is being sent to the program and how the program must react to process the data. At a fundamental level, all input (as well as output) is done on a character-by-character basis, as illustrated in Figure 9.12.

![](bbox=[0.223, 0.219, 0.776, 0.725])

Figure 9.12 shows, the entry of every piece of data, whether it's a string or a number, consists of typing characters. For example, the string Hello consists of pressing and releasing the five character keys H, e, l, o, and the Enter key. Similarly, output of the number 26 consists of displaying the five characters 2, ., 9, and 5. Although programmers typically do not think of data in this manner, programs are restricted to this character-by-character I/O, and all of C++s higher-level I/O functions and stream objects are based on lower-level I/O functions. These more elemental character functions, which can be used by a programmer, are listed in Table 9.6.