```
```cpp
//Postcondition: dvdTitle = title; movieStar1 = star1;
//              movieStar2 = star2;
//              movieProducer = producer;
//              movieDirector = director;
//              movieProductionCo = productionCo;
//              copiesInStock = setInStock;

        //Overload relational operators
        bool operator==(const dvdType&) const;
        bool operator!=(const dvdType&) const;
        bool operator<(const dvdType&) const;
        bool operator<=(const dvdType&) const;
        bool operator>(const dvdType&) const;
        bool operator>=(const dvdType&) const;

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

The definitions of the member functions of the class dvdType are the same as in Chapter 16. Because here we are overloading all of the relational operators, we give only the definitions of these member functions.

```
```cpp
        //Overload the relational operators
bool dvdType::operator==(const dvdType& right) const
{
    return (dvdTitle == right.dvdTitle);
}

bool dvdType::operator!=(const dvdType& right) const
{
    return (dvdTitle != right.dvdTitle);
}

bool dvdType::operator<(const dvdType& right) const
{
    return (dvdTitle < right.dvdTitle);
}
```
```