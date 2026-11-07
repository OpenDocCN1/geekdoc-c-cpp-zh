
```cpp
string director = "", string productionCo = "",
int setInStock = 0);
//constructor
//The member variables are set according to the
//incoming parameters. If no values are specified, the
//default values are assigned.
//Postcondition: videoTitle = title; movieStar1 = star1;
//               movieStar2 = star2;
//               movieProducer = producer;
//               movieDirector = director;
//               movieProductionCo = productionCo;
//               copiesInStock = setInStock;

//Overload the relational operators.
bool operator==(const videoType&) const;
bool operator!=(const videoType&) const;

private:
    string videoTitle;  //variable to store the name
                        //of the movie
    string movieStar1;  //variable to store the name
                        //of the star
    string movieStar2;  //variable to store the name
                        //of the star
    string movieProducer; //variable to store the name
                          //of the producer
    string movieDirector; //variable to store the name
                          //of the director
    string movieProductionCo; //variable to store the name
                              //of the production company
    int copiesInStock;  //variable to store the number of
                        //copies in stock
};
```

We leave the UML diagram of the class videoType as an exercise for you.

For easy output, we will overload the output stream insertion operator, <<, for the class videoType.

Next, we write the definitions of each function in the class videoType. The definitions of these functions, as given below, are quite straightforward and easy to follow.

```cpp
void videoType::setVideoInfo(string title, string star1,
                             string star2, string producer,
                             string director,
                             string productionCo,
                             int setInStock)
{
    videoTitle = title;
    movieStar1 = star1;
    movieStar2 = star2;
    movieProducer = producer;
    movieDirector = director;
    movieProductionCo = productionCo;
    copiesInStock = setInStock;
}

void videoType::checkOut()
{
    if (getNoOfCopiesInStock() > 0)
        copiesInStock--;
    else
        cout << "Currently out of stock" << endl;
}

void videoType::checkIn()
{
    copiesInStock++;
}

int videoType::getNoOfCopiesInStock() const
{
    return copiesInStock;
}

void videoType::printTitle() const
{
    cout << "Video Title: " << videoTitle << endl;
}

void videoType::printInfo() const
{
    cout << "Video Title: " << videoTitle << endl;
    cout << "Stars: " << movieStar1 << " and "
         << movieStar2 << endl;
    cout << "Producer: " << movieProducer << endl;
    cout << "Director: " << movieDirector << endl;
    cout << "Production Company: " << movieProductionCo
         << endl;
    cout << "Copies in stock: " << copiesInStock
         << endl;
}

bool videoType::checkTitle(string title)
{
    return(videoTitle == title);
}

void videoType::updateInStock(int num)
{
    copiesInStock += num;
}

void videoType::setCopiesInStock(int num)
{
    copiesInStock = num;
}

string videoType::getTitle() const
{
    return videoTitle;
}

videoType::videoType(string title, string star1,
                     string star2, string producer,
                     string director,
                     string productionCo, int setInStock)
{
    setVideoInfo(title, star1, star2, producer, director,
                 productionCo, setInStock);
}

bool videoType::operator==(const videoType& other) const
{
    return (videoTitle == other.videoTitle);
}

bool videoType::operator!=(const videoType& other) const
{
    return (videoTitle != other.videoTitle);
}

ostream& operator<< (ostream& osObject, const videoType& video)
{
    osObject << endl;
    osObject << "Video Title: " << video.videoTitle << endl;
    osObject << "Stars: " << video.movieStar1 << " and "
             << video.movieStar2 << endl;
    osObject << "Producer: " << video.movieProducer << endl;
    osObject << "Director: " << video.movieDirector << endl;
    osObject << "Production Company: "
             << video.movieProductionCo << endl;
    osObject << "Copies in stock: " << video.copiesInStock
             << endl;
    osObject << "__________________________________"
             << endl;

    return osObject;
}
```

## Video List

This program requires us to maintain a list of all of the videos in the store. We also should be able to add a new video to our list. In general, we would not know how many videos are in the store, and adding or deleting a video from the store would change the number of videos in the store. Therefore, we will use a linked list to create a list of videos (see Figure 18-46).

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1130_0.png)

**FIGURE 18-46**  *videoList*

Earlier in this chapter, we defined the class `unorderedLinkedList` to create a linked list of objects. We also defined the basic operations such as insertion and deletion of a video in the list. However, some operations are very specific to the video list, such as check out a video, check in a video, set the number of copies of a video, and so on. These operations are not available in the class `unorderedLinkedList`. We will, therefore, derive a class `videoListType` from the class `unorderedLinkedList` and add these operations.

The definition of the class `videoListType` is:

```cpp
/******************************************************************
// Author: D.S. Malik
//
// class videoListType
// This class specifies the members to implement a list of
// videos.
******************************************************************/

#include <string>
#include "unorderedLinkedList.h"
#include "videoType.h"

using namespace std;

class videoListType : public unorderedLinkedList<videoType>
{
public:
    bool videoSearch(string title) const;
        //Function to search the list to see whether a
        //particular title, specified by the parameter title,
        //is in the store.
        //Postcondition: Returns true if the title is found,
        //              and false otherwise.

    bool isVideoAvailable(string title) const;
        //Function to determine whether a copy of a particular
        //video is in the store.
        //Postcondition: Returns true if at least one copy of the
        //              video specified by title is in the store,
        //              and false otherwise.

    void videoCheckOut(string title);
        //Function to check out a video, that is, rent a video.
        //Postcondition: copiesInStock is decremented by one.

    void videoCheckIn(string title);
        //Function to check in a video returned by a customer.
        //Postcondition: copiesInStock is incremented by one.

    bool videoCheckTitle(string title) const;
        //Function to determine whether a particular video is in
        //the store.
        //Postcondition: Returns true if the video's title is
        //              the same as title, and false otherwise.
        //

    void videoUpdateInStock(string title, int num);
        //Function to update the number of copies of a video
        //by adding the value of the parameter num.
        //parameter title specifies the name of the video for
        //which the number of copies is to be updated.
        //Postcondition: copiesInStock = copiesInStock + num;

    void videoSetCopiesInStock(string title, int num);
        //Function to reset the number of copies of a video.
        //The parameter title specifies the name of the video
        //for which the number of copies is to be reset, and the
        //parameter num specifies the number of copies.
        //Postcondition: copiesInStock = num;

    void videoPrintTitle() const;
        //Function to print the titles of all the videos in
        //the store.

private:
    void searchVideoList(string title, bool& found,
                         nodeType<videoType>* &current) const;
    //This function searches the video list for a
    //particular video, specified by the parameter title.
    //Postcondition: If the video is found, the parameter
    //              found is set to true, otherwise it is set
    //              to false. The parameter current points
    //              to the node containing the video.
};
```

Note that the class videoListType is derived from the class unorderedLinkedList via a public inheritance. Furthermore, unorderedLinkedList is a class template, and we have passed the class videoType as a parameter to this class. That is, the class videoListType is
