
```cpp
void videoListType::videoPrintTitle() const
{
    nodeType<videoType>* current;

    current = first;
    while (current != NULL)
    {
        current->info.printTitle();
        current = current->link;
    }
}
```

## PART 2: CUSTOMER COMPONENT

### Customer Object

The customer object stores information about a customer, such as the first name, last name, account number, and a list of videos rented by the customer.

Every customer is a person. We have already designed the `class personType` in Example 11-9 (Chapter 11) and described the necessary operations on the name of a person. Therefore, we can derive the `class customerType` from the `class personType` and add the additional members that we need. First, however, we must redefine the `class personType` to take advantage of the new features of object-oriented design that you have learned, such as operator overloading, and then derive the `class customerType`.

Recall that the basic operations on an object of type `personType` are:

- 1. Print the name.
- 2. Set the name.
- 3. Show the first name.
- 4. Show the last name.

Similarly, the basic operations on an object of type `customerType` are:

- 1. Print the name, account number, and the list of rented videos.
- 2. Set the name and the account number.
- 3. Rent a video; that is, add the rented video to the list.
- 4. Return a video; that is, delete the rented video from the list.
- 5. Show the account number.

The details of implementing the customer component are left as an exercise for you. (See Programming Exercise 14 at the end of this chapter.)

### Main Program

We will now write the main program to test the video object. We assume that the necessary data for the videos are stored in a file. We will open the file and create the list of videos owned by the video store. The data in the input file is in the following form:

```
video title (that is, the name of the movie)
movie star1
movie star2
movie producer
movie director
movie production co.
number of copies
.
.
.
```

We will write a function, createVideoList, to read the data from the input file and create the list of videos. We will also write a function, displayMenu, to show the different choices—such as check in a movie or check out a movie—that the user can make. The algorithm of the function main is:

- 1. Open the input file.
  - If the input file does not exist, exit the program.
- 2. Create the list of videos (createVideoList).
- 3. Show the menu (displayMenu).
- 4. While not done
  Perform various operations.

Opening the input file is straightforward. Let us describe Steps 2 and 3, which are accomplished by writing two separate functions: createVideoList and displayMenu.

**createVideoList** This function reads the data from the input file and creates a linked list of videos. Because the data will be read from a file and the input file was opened in the function main, we pass the input file pointer to this function. We also pass the video list pointer, declared in the function main, to this function. Both parameters are reference parameters. Next, we read the data for each video and then insert the video in the list. The general algorithm is:

- a. Read the data and store it in a video object.
- b. Insert the video in the list.
- c. Repeat steps a and b for each video’s data in the file.

**displayMenu** This function informs the user what to do. It contains the following output statements:

Select one of the following:

- 1. To check whether the store carries a particular video
- 2. To check out a video
- 3. To check in a video
- 4. To check whether a particular video is in stock
- 5. To print only the titles of all the videos
- 6. To print a list of all the videos
- 9. To exit

In pseudocode, Step 4 (of the main program) is:

- a. get choice
- b.

```cpp
    while (choice != 9)
    {
        switch (choice)
        {
        case 1:
            a. get the movie name
            b. search the video list
            c. if found, report success
                else report "failure"
            break;
        case 2:
            a. get the movie name
            b. search the video list
            c. if found, check out the video
                else report "failure"
            break;
        case 3:
            a. get the movie name
            b. search the video list
            c. if found, check in video
                else report "failure"
            break;
        case 4:
            a. get the movie name
            b. search the video list
            c. if found
                if number of copies > 0
                    report "success"
                else
                    report "currently out of stock"
            else report "failure"
            break;
        case 5:
            print the titles of the videos
            break;
        case 6:
            print all the videos in the store
            break;
        default: bad selection
        } //end switch

        displayMenu();
        get choice;
    }//end while
```

## PROGRAM LISTING

```cpp
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

        //process the requests
        while (choice != 9)
        {
            switch (choice)
            {
            case 1:
                cout << "Enter the title: ";
                getline(cin, title);
                cout << endl;

                if (videoList.videoSearch(title))
                    cout << "The store carries " << title
                         << endl;
                else
                    cout << "The store does not carry "
                         << title << endl;
                break;

            case 2:
                cout << "Enter the title: ";
                getline(cin, title);
                cout << endl;

                if (videoList.videoSearch(title))
                {
                    if (videoList.isVideoAvailable(title))
                    {
                        videoList.videoCheckout(title);
                        cout << "Enjoy your movie:"
                             << title << endl;
                    }
                    else
                        cout << "Currently " << title
                             << " is out of stock." << endl;
                }
                else
                    cout << "The store does not carry "
                         << title << endl;
                break;

            case 3:
                cout << "Enter the title: ";
                getline(cin, title);
                cout << endl;

                if (videoList.videoSearch(title))
                {
                    videoList.videoCheckIn(title);
                    cout << "Thanks for returning "
                         << title << endl;
                }
                else
                    cout << "The store does not carry "
                         << title << endl;
                break;

            case 4:
                cout << "Enter the title: ";
                getline(cin, title);
                cout << endl;

                if (videoList.videoSearch(title))
                {
                    if (videoList.isVideoAvailable(title))
                        cout << title << " is currently in "
                             << "stock." << endl;
                    else
                        cout << title << " is currently out "
                             << "of stock." << endl;
                }
                else
                    cout << "The store does not carry "
                         << title << endl;
                break;

            case 5:
                videoList.videoPrintTitle();
                break;

            case 6:
                videoList.print();
                break;

            default:
                cout << "Invalid selection." << endl;
            }//end switch

            displayMenu();    //display menu

            cout << "Enter your choice: ";
            cin >> choice;     //get the next request
            cin.get(ch);
            cout << endl;
        }//end while

        return 0;
}
```
