```
```cpp
void videoCheckOut(string title);
    //Function to check out a video, that is, rent a video.
    //Postcondition: copiesInStock is decremented by one.

void videoCheckIn(string title);
    //Function to check in a video returned by a customer.
    //Postcondition: copiesInStock is incremented by one.

bool videoCheckTitle(string title) const;
    //Function to determine whether a particular video is in
    //the store.
    //Postcondition: Returns true if the video’s title is
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
```

Note that the class videoListType is derived from the class unorderedLinkedList via a public inheritance. Furthermore, unorderedLinkedList is a class template, and we have passed the class videoType as a parameter to this class. That is, the class videoListType is