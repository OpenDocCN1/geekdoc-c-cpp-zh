Figure 15.2 copies a file one character at a time into another file. Assume that the executable file for this program is called mycopy. A typical command line for executing this program is

mycopy input output

This command line indicates that the file input should be copied to the file output. When the program executes, if argc is not 3 (mycopy counts as one of the arguments), the program prints an error message (line 8) and terminates. Otherwise, the array argv contains the strings "mycopy", "input" and "output". This program uses its second and third command-line arguments as filenames.

```
// fig15_02.c
// Using command-line arguments
#include <stdio.h>

int main(int argc, char *argv[]) {
    // check number of command-line arguments
    if (argc != 3) {
        puts("Usage: mycopy infile outfile");
    }
    else {
        FILE *inFilePtr = NULL; // input file pointer

        // try to open the input file
        if ((inFilePtr = fopen(argv[1], "r")) != NULL) {
            FILE *outFilePtr = NULL; // output file pointer

            // try to open the output file
            if ((outFilePtr = fopen(argv[2], "w")) != NULL) {
                int c = 0; // holds characters read from source file

                // read and output characters
                while ((c = fgetc(inFilePtr)) != EOF) {
                    fputc(c, outFilePtr);
                }

                fclose(outFilePtr); // close the output file
            }
            else { // output file could not be opened
                printf("File \"%s\" could not be opened\n", argv[2]);
            }

            fclose(inFilePtr); // close the input file
        }
        else { // input file could not be opened
            printf("File \"%s\" could not be opened\n", argv[1]);
        }
    }
}
```