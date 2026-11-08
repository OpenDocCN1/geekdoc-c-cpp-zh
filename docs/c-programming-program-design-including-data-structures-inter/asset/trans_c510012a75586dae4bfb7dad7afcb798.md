
## 编程示例：DVD 商店（再探）

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1388_0.png)

### DVD 对象

在第 16 章中，我们设计了一个程序，帮助 DVD 商店自动化其 DVD 租赁流程。该程序使用一个（无序）链表来跟踪商店中的 DVD 库存。由于链表上的搜索算法是顺序的，而且链表相当大，搜索可能很耗时。本章中，你学习了如何在二叉树中组织数据。如果二叉树构造良好（即不是线性的），那么搜索算法可以显著改进。此外，通常二叉搜索树中的项插入和删除比链表中更快。因此，我们将重新设计 DVD 商店程序，以便 DVD 库存可以在二叉树中维护。与第 16 章一样，我们将客户列表设计为二叉树的工作留作练习。

在第 16 章中，使用链表维护商店中的 DVD 列表。由于链表是无序的，为了查看特定 DVD 是否有库存，顺序搜索算法使用相等运算符进行比较。然而，在二叉搜索树的情况下，我们需要其他关系运算符来进行搜索、插入和删除操作。因此，我们将重载所有关系运算符。除了这个差异之外，类 `dvdType` 与之前相同。不过，为了完整起见，我们给出它的定义。

```cpp
//***************************************************************
// Author: D. S. Malik
//
// class dvdType
// This class specifies the members to implement a DVD. It
// overloads the stream insertion operator and relational
// operators.
//***************************************************************

class dvdType
{
    friend ostream& operator<< (ostream&, const dvdType&);

public:
    void setDVDInfo(string title, string star1,
                    string star2, string producer,
                    string director, string productionCo,
                    int setInStock);
    //Function to set the details of a DVD.
    //The member variables are set according to the
    //parameters.
    //Postcondition: dvdTitle = title; movieStar1 = star1;
    //               movieStar2 = star2;
    //               movieProducer = producer;
    //               movieDirector = director;
    //               movieProductionCo = productionCo;
    //               copiesInStock = setInStock;

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

类 `dvdType` 的成员函数定义与第 16 章相同。由于这里我们重载所有关系运算符，我们只给出这些成员函数的定义。

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

bool dvdType::operator<=(const dvdType& right) const
{
    return (dvdTitle <= right.dvdTitle);
}

bool dvdType::operator>(const dvdType& right) const
{
    return (dvdTitle > right.dvdTitle);
}

bool dvdType::operator>=(const dvdType& right) const
{
    return (dvdTitle >= right.dvdTitle);
}
```

### DVD 列表

DVD 列表维护在二叉搜索树中。因此，我们从类 `bSearchTreeType` 派生类 `dvdBinaryTree`。类 `dvdBinaryTree` 的定义如下：

```cpp
/***************************************************************
// Author: D. S. Malik
//
// class dvdBinaryTree
// This class extends the class bSearchTreeType to create
// a DVD list.
//***************************************************************

class dvdBinaryTree: public bSearchTreeType<dvdType>
{
public:
    bool dvdSearch(string title);
        //Function to search the list to see whether a
        //particular title, specified by the parameter title,
        //is in the store.
        //Postcondition: Returns true if the title is found,
        //              and false otherwise.

    bool isDVDAvailable(string title);
        //Function to determine whether a copy of a particular
        //DVD is in the store.
        //Postcondition: Returns true if at least one copy of
        //              the DVD specified by title is in the
        //              store, and false otherwise.

    void dvdCheckIn(string title);
        //Function to check in a DVD returned by a customer.
        //Postcondition: copiesInStock is incremented by one.

    void dvdCheckOut(string title);
        //Function to check out a DVD, that is, rent a DVD.
        //Postcondition: copiesInStock is decremented by one.

    bool dvdCheckTitle(string title) const;
    //Function to determine whether a particular DVD is in
    //the store.
    //Postcondition: Returns true if the DVD's title is
    //              the same as title, and false otherwise.

    void dvdUpdateInStock(string title, int num);
    //Function to update the number of copies of a DVD
    //by adding the value of the parameter num. The
    //parameter title specifies the name of the DVD for
    //which the number of copies is to be updated.
    //Postcondition: copiesInStock = copiesInStock + num;

    void dvdSetCopiesInStock(string title, int num);
    //Function to reset the number of copies of a DVD.
    //The parameter title specifies the name of the DVD
    //for which the number of copies is to be reset, and
    //the parameter num specifies the number of copies.
    //Postcondition: copiesInStock = num;

    void dvdPrintTitle() const;
    //Function to print the titles of all the DVDs in
    //the store.

private:
    void searchDVDList(string title, bool& found,
                       nodeType<dvdType>*& current) const;
    //This function searches the DVD list for a
    //particular DVD, specified by the parameter title.
    //If the DVD is found, the parameter found is set to
    //true, otherwise false; the parameter current points
    //to the node containing the DVD.

    void inorderTitle(nodeType<dvdType>* p) const;
    //This function prints the titles of all the DVDs
    //in stock.
};
```

类 `dvdBinaryTree` 的成员函数 `isDVDAvailable`、`dvdCheckIn`、`dvdCheckOut`、`dvdCheckTitle`、`dvdUpdateInStock`、`dvdSetCopiesInStock` 和 `dvdSearch` 的定义与第 16 章给出的这些函数的定义相似。唯一的区别在于，这里它们是类 `dvdBinaryTree` 的成员。你可以在本书配套网站上找到这些函数的完整定义。接下来，我们讨论类 `dvdBinaryTree` 其余函数的定义。

函数 `searchDVDList` 使用的搜索算法类似于本章前面给出的二叉搜索树搜索算法。如果在列表中找到搜索项，则返回 `true`。它还返回一个指向包含搜索项的节点的指针。该函数的定义如下：
