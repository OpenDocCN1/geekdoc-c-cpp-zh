# Display 12.7 Formatting Output (part 3 of 3)

Sample Dialogue

# Rawdata.txt
(Not changed by program)

```
10.37    -9.89897
2.313   -8.950   15.0

7.33333   92.8765
-1.237568432e2
```

# neat.txt
(After program is run)

```
+10.37000
-9.89897
+2.31300
-8.95000
+15.00000
+7.33333
+92.87650
-123.75684
```

# Screen Output

```
+10.37000
-9.89897
+2.31300
-8.95000
+15.00000
+7.33333
+92.87650
-123.75684
End of program.
```

# EXAMPLE: Editing a Text File

The program discussed here is a very simple example of text editing applied to files. This program can be used to automatically generate C++ advertising material from existing C advertising material (in a rather simplistic way). The program takes its input from a file that contains advertising copy that says good things about C and writes similar advertising copy about C++ in another file. The file that contains the C advertising copy is called cad.txt, and the new file that receives the C++ advertising copy is called cppad.txt. The program is shown in Display 12.8. The program simply reads every character in the file cad.txt and copies the characters to the file cppad.txt. Every character is copied unchanged, except that when the uppercase letter 'C' is read from the input file, the program writes the string "C++" to the output file. This program assumes that whenever the letter 'C' occurs in the input file, it names the C programming language; so this change is exactly what is needed to produce the updated advertising copy.

Notice that the line breaks are preserved when the program reads characters from the input file and writes the characters to the output file. The newline character '\n' is treated just like any other character. It is read from the input file with the member function get, and it is written to the output file using the insertion operator, <<. We must use the member function get to read the input (rather than the extraction operator, >>) because we want to read whitespace.