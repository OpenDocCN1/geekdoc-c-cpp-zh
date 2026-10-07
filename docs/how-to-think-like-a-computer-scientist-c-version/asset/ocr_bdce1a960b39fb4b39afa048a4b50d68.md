# 15.3. FILE OUTPUT

```
cout << line << endl;
}
```

The function c.str converts an apstring to a native C string. Because the ifstream constructor accepts a C string as an argument, we have to convert the apstring.

Immediately after opening the file, we invoke the good function. The return value is false if the system could not open the file, most likely because it does not exist, or if you do not have permission to read it.

The statement while(true) is an idiom for an infinite loop. Usually there will be a break statement in the loop so that the program does not run forever (although some programs do). In this case, the break statement allows us to exit the loop as soon as we detect the end of file.

It is important to exit the loop between the input statement and the output statement, so when getline fails at the end of the file, we do not output the invalid data in line.

# 15.3 File input

Sending output to a file is similar. For example, we could modify the program to copy lines from one file to another.

```
infile("input-file");
outfile("output-file");
```

```
if (infile.good() == false || outfile.good() == false) {
cout << "Unable to open one of the files." << endl;
exit(1);
}
```

```
while (true) {
getline(infile, line);
if (infile.eof()) break;
outfile << line << endl;
}
```

# 15.4 Parsing input

In Section 14 I defined "parsing" as the process of analyzing the structure of a sentence in a natural language or a statement in a formal language. For example, the compiler can parse your program before it can translate it into machine language.

In addition, when you read input from a file or from the keyboard you often to parse it in order to extract the information you want and detect errors.