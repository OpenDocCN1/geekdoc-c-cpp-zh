
```
convertP6ToP3(fin, fout, image, imageInfo) :
  read_header(fin, fout, imageInfo)
  readAndWriteImageData(fin, fout, image, width, height);
```

```
smooth(image, width, height):
  set i to 1
  set j to 1
  while(i<height-1)
    while(j<width-1)
      image[i][j] = (image[i][j-1] + image[i-1][j]
        + image[i][j+1] + image[i+1][j])/4
```

```
writeP3Image(ofstream& out, vector<vector<Pixel> > &image, char comment[], int maxColor):
  writeHeader()
  for all rows
    for all columns
      write image[row][col]
```

```
readAndWriteImageData(ifstream& fin, ofstream& fout,
  vector<vector<Pixel> > &image,
  int w, int h):
  allocate w rows of memory for image
  for all w
    allocate h columns
    for all h
      read red byte
      read green byte
      read blue byte
      convert bytes to unsigned int
      image[i][j]=Pixel(red,green,blue)
```

```
writeHeader(ofstream& fout, char magicNumber[],
  char comment[], int w, int h,
  int maxPixelVal):
  output magicNumber
  output comment
  output w h maxPixelVal
```

```
read_header(fin, fout, imageInfo) :
  read magic_num
  if(magic number is not P6) exit(1)
  get next line of header
  do
    {
      if(next_ch == '#')
        save comment line
        get next line of header
      else
        look for digits
        if digits found
          save decimal value
          increment info count
        else
          get next line of header
    while(!fin.eof() && infoCount<3)
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
                int imageInfo[]);
void writeP3Image(ofstream& out,
                  vector<vector<Pixel> > &image,
                  char comment[], int maxColor);
```

/**-------------------------------------------------------------*/
/** filename main.cpp                                           */
/** Program chapter10_4                                         */
/**                                                             */
/** This program converts a PPM file from a P6 format           */
/** to a P3 format.  A smoothing operation is performed         */
/** on the converted image and the smoothed image               */
/** is written to a new file.                                   */
/**-------------------------------------------------------------*/
#include "ImageFunctions.h"
using namespace std;

int main()
{
   //Define objects
   char filename[MAXLEN];
   ifstream fin;
   ofstream fout,sout;
   int imageInfo[3];             //w,h,maxColor
   vector< vector<Pixel> > image;//pixel grid
   char comment[MAXLEN] = "#";

   //Open files
   openIOFiles(fin,fout,filename);

   //Convert binary file
   convertP6toP3(fin, fout, image, imageInfo);

   //Perform smoothing operation on image
   smooth(image);

   //Generate a meaningful filename and comment
   //Terminate input file name at .
   char * loc = strchr(filename,'.');
   *loc = '\0';

   //Add extension to name
   strcat(filename,"P3Smoothed.ppm");

   //Open file for output
   sout.open(filename);

   //Create a comment for the smoothed image
   strcat(comment,filename);
   writeP3Image(sout, image, comment, imageInfo[2]);
   cout << "P3 Image written to "<< filename << "\nGoodbye." << endl;
   //close all files
   fout.close();
   sout.close();
   fin.close();
   return 0;
}
```

```
//filename imageFunctions.cpp
void openIOFiles(ifstream& fin, ofstream& fout, char
                 inputFilename[])
{
   //Define filestreams
   char outputFilename[MAXLEN];
   int i;
   //Prompt user for input file
   cout << "Enter file name ";
   cin >> inputFilename;
   //Open .ppm binary file for input
   fin.open(inputFilename, ios::binary);
   if(!fin)
   {
      cout << "Can not open input file: goodbye";
      exit(1);
   }
   //Generate meaningful output filename
   strcpy(outputFilename,inputFilename);
   //Terminate output filename at .
   char * loc = strchr(outputFilename,'.');
   *loc = '\0';
   //Add extension to name
   strcat(outputFilename,"P3.ppm");
   //Open .ppm ascii file for output
   fout.open(outputFilename);
}

if(!fout)
{
    cout << "can not open output file: goodbye";
    exit(1);
}
}

void convertP6toP3(ifstream& bin, ofstream& out,
                   vector<vector<Pixel> > &image, int info[])
{
    readHeader(bin,out, info);
    int width=info[0], height=info[1];
    readAndWriteImageData(bin,out,image,width,height);
}

void smooth(vector< vector<Pixel> > &image)
{
    int h = image.size();
    int w = image[0].size();

    Pixel sum;
    for(int i=1; i<(h-1); i++)
    for(int j=1; j<(w-1); j++)
    {
        sum = image[i+1][j] + image[i-1][j]
            + image[i][j+1] + image[i][j-1];
        sum = sum/4;
        image[i][j] = sum;
    }
}

void writeP3Image(ofstream& out, vector<vector<Pixel> > &image,
                  char comment[], int maxColor)
{
    int h,w,pCount;
    char magicNumber[3] = "P3";
    w = (int)image.size();
    h = (int)image[0].size();
    writeHeader(out,magicNumber,comment,w,h,maxColor);
    for(int i=0; i<h; ++i)
    {
        for(int j=0; j<w; ++j)
        {
            out << image[i][j];
            ++pCount;
            if (pCount == 10)
            {
               out << newline;
               pCount = 0;
            }
            else
               out << ' ';
        }
    }
}

void readAndWriteImageData(ifstream& fin, ofstream& fout,
                           vector<vector<Pixel> > &image,
                           int w, int h)
{
   //Read and write image data
   //Define input variables
   int charCnt=0;
   char colorByte;
   unsigned char aChar;
   unsigned int triple[3]; //red, green, blue

   //Allocate memory
   image.resize(h); //allocate h rows
   for (int i = 0; i < h; i++)
   {
      image[i].resize(w); //for each row, allocate w columns
      for (int j = 0; j < w; ++j)
      {
         for(int k=0; k<3; ++k)
         {
            //read one byte
            fin.read(&colorByte, 1);
            //convert to unsigned char
            aChar = (unsigned char)colorByte;
            //save as unsigned int
            triple[k] = (unsigned int)aChar;
            //write as int
            fout << triple[k] << ' ';
         }
         //end for k
         image[i][j].setPixel(triple[0],triple[1],triple[2]);
         //CR printed ever 32 pixels
         ++charCnt;
         if (charCnt == 32)
         {
            fout << newline;
            charCnt=0;
         }
      }
   }
}

void readHeader(ifstream& fin, ofstream& fout, int imageInfo[])
{
    //Define and initialize input variables
    char bData[MAXLEN]={0},magicNumber[MAXWIDTH],
    comment[MAXLEN]={'#'};
    int bIndex=0, charCount=0, infoCount=0;
    char ch, aNumber[MAXWIDTH];
    //Input first line of text header(magic number)
    //If the magic number is not P6, exit program
    fin.getline(magicNumber,3);
    if (strcmp(magicNumber, "P6") != 0)
    {
    cout << "Unexpected file format\n";
    exit(1);
    }
    //Clear bData array and reset bIndex
    //Input next line of text header
    strcpy(bData, "");
    bIndex=0;
    fin.getline(bData,MAXLEN);
    do
    {
    //is this the beginning of a comment
    ch = bData[bIndex];
    if(ch == '#')
    {
    //Comment has been read.
    //Get all characters until a newline is found
    charCount=0;
    while(ch != newline && charCount < MAXLEN)
    {
    comment[charCount] = ch;
    ++bIndex;
    ++charCount;
    }
    }
    if(charCount == MAXLEN && ch != newline)
    {
    cout << "Comment exceeded maximum length of "
    << MAXLEN << endl;
    exit(1);
    }
