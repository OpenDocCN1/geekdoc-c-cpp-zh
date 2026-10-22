```
{
    ID = 3,
    Title = "Title 3",

AuthorName = "Author 1",
YearOfPublication = 2017
},
new Book()
{
    ID = 4,
    Title = "Title 4",

AuthorName = "Author 3",
YearOfPublication = 1999
},
new Book()
{
    ID = 5,
    Title = "Title 5",

AuthorName = "Author 4",
YearOfPublication = 2017
},
};
```

One query we might want to run is this query using a group by query. A group by query has the following format:

```
var results = from collectionVar in
collectionName
group collectionBar by collectionVar.
PropertyName
    into varGroupName
```