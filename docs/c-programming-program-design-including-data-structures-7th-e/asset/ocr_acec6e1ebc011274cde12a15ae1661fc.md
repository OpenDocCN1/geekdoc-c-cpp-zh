```
```cpp
string director = "", string productionCo = "",
int setInStock = 0);
//constructor
//The member variables are set according to the
//incoming parameters. If no values are specified, the
//default values are assigned.
//Postcondition: dvdTitle = title; movieStar1 = star1;
//               movieStar2 = star2;
//               movieProducer = producer;
//               movieDirector = director;
//               movieProductionCo = productionCo;
//               copiesInStock = setInStock;

//Overload the relational operators
bool operator==(const dvdType&) const;
bool operator!=(const dvdType&) const;

private:
    string dvdTitle;       //variable to store the name
                           //of the movie
    string movieStar1;     //variable to store the name
                           //of the star
    string movieStar2;     //variable to store the name
                           //of the star
    string movieProducer;  //variable to store the name
                           //of the producer
    string movieDirector;  //variable to store the name
                           //of the director
    string movieProductionCo; //variable to store the name
                              //of the production company
    int copiesInStock;     //variable to store the number of
                           //copies in stock
};
```
```

We leave the UML diagram of the class `dvdType` as an exercise for you.

For easy output, we will overload the output stream insertion operator, `<<`, for the class `dvdType`.

Next, we will write the definitions of each function in the class `dvdType`. The definitions of these functions, as given below, are quite straightforward and easy to follow.

```
```cpp
void dvdType::setDVDInfo(string title, string star1,
                          string star2, string producer,
                          string director,
                          string productionCo,
                          int setInStock)
{
    dvdTitle = title;
    movieStar1 = star1;
```
```