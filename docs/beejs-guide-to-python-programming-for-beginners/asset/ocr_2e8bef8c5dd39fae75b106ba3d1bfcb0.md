Here's the file we want to read¹¹. Look through it and see how all the information for a particular record is in each row:

```
Title,Release Year,Studio,Publisher
Minecraft,2011,Mojang,Microsoft Studios
M.U.L.E.,1983,Ozark Softscape,Activision
X-Men The Official Game,2006,Z-AXIS,Activision
Populous,1989,Bullfrog Productions,Electronic Arts
DOOM,1993,id Software,id Software
Lemmings,1991,DMA Design,Psygnosis
```

Your goal is to read the file and store each record in an object. (Make a class that defines the same fields you have in the CSV file to instantiate the objects from.)

Then print out the data, like so:

```
M.U.L.E.          1983    Ozark Softscape    Activision
Populous         1989    Bullfrog Productions Electronic Arts
Lemmings         1991    DMA Design         Psygnosis
DOOM             1993    id Software        id Software
X-Men The Official Game 2006 Z-AXIS           Activision
Minecraft        2011    Mojang             Microsoft Studios
```

The printout, above, is shown in sorted-by-year order. That's a stretch goal if you want to take it on. (Hint: check out the key keyword argument to the .sort() method. Also, the solution code talks about it in detail.)

Also, incidentally, M.U.L.E.¹² is one of the greatest games ever written. Despite it being over 25 years old, PC World magazine rated it the 5th-greatest game of all time in 2009. If you haven't played it, grab an Atari 800 emulator, four gamepads, and four friends, and have some fun. (Or play solo against the computer.)

Now, a quick word of warning: this exercise assumes you're going to implement the logic for parsing this file yourself. But in real life, in Python, you'd never do this. Python has built-in functionality to parse CSV files, and it's far more robust and correct than what we're doing here. We're just reinventing the wheel in this case as a programming exercise.

Notice that the first line of the CSV file is a header. It describes what the columns are, but isn't actual data. You'll have to skip this line when you're reading the file. (Hint: call the next() function on the file iterator returned by open() to get the next line one time at the beginning.) (Solution¹³.)

3. Modify your multiplication table generator from the chapter on strings to save the table to disk instead of printing it to the screen.

The program should accept both the dimension of the table and the output filename on the command line, e.g.:

```
python multtablefile.py 12 table12x12.txt
```

4. Write a program to count the number of words in a file specified on the command line. The number of words should be printed out.