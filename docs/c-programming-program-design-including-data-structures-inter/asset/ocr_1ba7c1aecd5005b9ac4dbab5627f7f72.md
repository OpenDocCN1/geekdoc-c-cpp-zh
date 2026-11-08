```
```cpp
int getNoOfCopiesInStock() const;
//Function to check the number of copies in stock.
//Postcondition: The value of copiesInStock is returned.

void checkOut();
//Function to rent a DVD.
//The number of copies in stock is decremented by one.
//Postcondition: copiesInStock--;

void checkIn();
//Function to check in a DVD.
//The number of copies in stock is incremented by one.
//Postcondition: copiesInStock++;

void printTitle() const;
//Function to print the title of a movie.

void printInfo() const;
//Function to print the details of a DVD.
//Postcondition: The title of the movie, stars, director,
//              and so on are output on the screen.

bool checkTitle(string title);
//Function to check whether the title is the same as the
//title of the DVD.
//Postcondition: Returns the value true if the title is
//              the same as the title of the DVD, and
//              false otherwise.

void updateInStock(int num);
//Function to increment the number of copies in stock by
//adding the value of the parameter num.
//Postcondition: copiesInStock = copiesInStock + num;

void setCopiesInStock(int num);
//Function to set the number of copies in stock.
//Postcondition: copiesInStock = num;

string getTitle() const;
//Function to return the title of the DVD.
//Postcondition: The title of the DVD is returned.

dvdType(string title = "", string star1 = "",
        string star2 = "", string producer = "",
        string director = "", string productionCo = "",
        int setInStock = 0);
//Constructor
//The member variables are set according to the incoming
//parameters. If no values are specified, the default
//values are assigned.
```
```