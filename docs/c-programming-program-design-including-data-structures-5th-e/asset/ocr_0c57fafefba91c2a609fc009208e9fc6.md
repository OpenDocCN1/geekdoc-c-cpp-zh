# PROGRAM LISTING

```
```cpp
displayMenu();
    get choice;
}//end while

/************************************************************
// Author: D.S. Malik
//
// This program uses the classes videoType and videoListType to
// create a list of videos for a video store. It also performs
// basic operations such as check in and check out videos.
//************************************************************

#include <iostream>
#include <fstream>
#include <string>
#include "videoType.h"
#include "videoListType.h"

using namespace std;

void createVideoList(ifstream& infile,
                    videoListType& videoList);
void displayMenu();

int main()
{
        videoListType videoList;
        int choice;
        char ch;
        string title;

        ifstream infile;

                //open the input file
        infile.open("videoData.txt");
        if (!infile)
        {
                cout << "The input file does not exist. "
                     << "The program terminates!!!" << endl;
                return 1;
        }

                //create the video list
        createVideoList(infile, videoList);
        infile.close();

                //show the menu
        displayMenu();
        cout << "Enter your choice: ";
                         //get the request
        cin >> choice;
        cout << endl;
```
```