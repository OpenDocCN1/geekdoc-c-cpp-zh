```
while(i<height)
    while(j<width)
        image[i][j] = (image[i][j] + image[i][j-1] + image[i-1][j]
            + image[i][j+1] + image[i+1][j])/5
```

We are now ready to convert the pseudocode to C++:

```
/*
* Program chapter10_4
*
* This program reads an ASCII digital image and perform a
* smoothing operation on the on the image. The smoothed image
* is written to a new file.
*/

#include "Pixel.h"
#include <fstream>//Required for ifstream, ofstream
#include <string>//Required for string
#include <vector>//Required for vector
using namespace std;

//Function prototypes.
void read_header(istream& fin, ostream& fout,
    int& width, int& height, int& max);
void smooth(vector <vector<Pixel> >& , int w, int h);

int main()
{
    // Declare objects.
    int height, width, max, i, j;
    string filename;
    ifstream fin;
    ofstream fout;

    // Prompt user for file name and open file for input.
    cout << "Enter name of input file ";
    cin >> filename;
    fin.open(filename.c_str());
    if(fin.fail())
    {
        cerr << "Error opening input file\n";
    }
    else
    {
    // Open new file for output.
    filename = "smoothed." + filename;
    fout.open(filename.c_str());

    // Read and write header information.
    read_header(fin,fout, width, height, max);
```