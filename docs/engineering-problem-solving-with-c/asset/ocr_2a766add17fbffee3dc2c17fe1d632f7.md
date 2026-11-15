```
look for digits
if digits found
  save decimal value
  increment info count
else
  get next line of header
while(!fin.eof() && infoCount<3))
}
```

We are now ready to write our C++ solution. We will create a header file named imageFunctions.h for our include statements, function prototypes, and defined constants. A second file named imageFunctions.cpp will be created for the function definition and a file named main.cpp will be created for the main program. All files are provided below:

```
//file imageFunctions.h
#ifndef IMAGEFUNCTIONS
#define IMAGEFUNCTIONS

#include <cstdlib>
#include "Pixel.h"
#include <iostream>
#include <fstream>
#include <vector>

//Declared constants
const int MAXWIDTH(5); //max digits allowed for width
const int MAXLEN(100); //char array size
const char newline('\n');
const char nullChar('\0');

//Function prototypes
void openIOFiles(ifstream& fin, ofstream& fout,
                 char filename[]);
void convertP6toP3(ifstream& bin, ofstream& out,
                   vector<vector<Pixel> > &image,
                   int info[]);
void readAndWriteImageData(ifstream& fin, ofstream& fout,
                           vector<vector<Pixel> > &image,
                           int w, int h);
void readHeader(ifstream& fin, ofstream& fout,
                imageInfo[]);
void writeP3Image(ofstream& out,
                  vector<vector<Pixel> > &image,
                  char comment[], int maxColor);
```