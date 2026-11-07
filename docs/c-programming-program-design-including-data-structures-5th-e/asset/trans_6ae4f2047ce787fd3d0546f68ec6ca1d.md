
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
    //Postcondition: Returns true if the video's title is
    //              the same as title, and false otherwise.
    //

void videoUpdateInStock(string title, int num);
    //Function to update the number of copies of a video
    //by adding the value of the parameter num. The
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

注意，类 `videoListType` 通过公有继承派生自类 `unorderedLinkedList`。此外，`unorderedLinkedList` 是一个类模板，并且我们已经将类 `videoType` 作为参数传递给该类。也就是说，类 `videoListType` 不是模板。因为我们现在处理的是一个非常具体的数据类型，所以 `class videoListType` 不再需要是模板。因此，链表中每个节点的 `info` 类型现在是 `videoType`。通过 `class videoType` 的成员函数，现在可以访问某些成员——例如，`videoType` 类型对象的 `videoTitle` 和 `copiesInStock`。

接下来给出实现 `class videoListType` 操作的函数定义。

视频列表上的主要操作是归还视频和借出视频。这两种操作都需要搜索列表，并在视频列表中找到正在归还或借出的视频的位置。其他操作，例如确定某个视频是否在商店中、更新某个视频的副本数量等，也需要搜索列表。为了简化搜索过程，我们将编写一个函数，用于在视频列表中搜索特定视频。如果找到该视频，它将参数 `found` 设置为 true，并返回指向该视频的指针，以便可以执行视频对象的归还、借出及其他操作。注意，函数 `searchVideoList` 是 `class videoListType` 的私有数据成员，因为它仅用于内部操作。首先，我们描述搜索过程。

考虑图 17-47 所示的视频列表节点。

![](img/f97f778697507bb6fdd80c5991210cba_1101_0.png)

**图 17-47** 视频列表的节点

组件 `info` 的类型为 `videoType`，包含有关视频的必要信息。实际上，节点的组件 `info` 有七个成员：`videoTitle`、`movieStar1`、`movieStar2`、`movieProducer`、`movieDirector`、`movieProductionCo` 和 `copiesInStock`。（参见 `class videoType` 的定义。）因此，视频列表的节点具有图 17-48 所示的形式。

![](img/f97f778697507bb6fdd80c5991210cba_1102_0.png)

**图 17-48** 显示 `info` 各组成部分的视频列表节点

这些成员变量都是私有的，不能直接访问。类 videoType 的成员函数将帮助我们检查和/或设置特定组件的值。

假设有一个指针——比如 `current`——指向视频列表中的一个节点（见图 17-49）。

![](img/f97f778697507bb6fdd80c5991210cba_1102_1.png)

**图 17-49** 指针 `current` 和视频列表节点

现在：

```
current->info
```

指的是节点的 `info` 部分。假设我们想知道存储在该节点中的视频标题是否与变量 `title` 指定的标题相同。表达式：

```
current->info.checkTitle(title)
```

如果存储在该节点中的视频标题与参数 `title` 指定的标题相同，则为 true，否则为 false。（注意，成员函数 `checkTitle` 是一个值返回函数。参见它在类 `videoType` 中的声明。）

作为另一个例子，假设我们要将该节点的 `copiesInStock` 设置为 10。因为 `copiesInStock` 是私有成员，不能直接访问。因此，语句：

```
current->info.copiesInStock = 10;    //illegal
```

是不正确的，并且会产生编译时错误。我们必须按如下方式使用成员函数 `setCopiesInStock`：

```
current->info.setCopiesInStock(10);
```

既然我们知道了如何访问存储在节点中的视频的成员变量，下面描述搜索视频列表的算法。

```
while (not found)
    if the title of the current video is the same as the desired
       title, stop the search
    else
        check the next node
```

下面的函数定义执行所需的搜索。

```cpp
void videoListType::searchVideoList(string title, bool& found,
                                      nodeType<videoType>* &current) const
{
    found = false;    //set found to false

    current = first;  //set current to point to the first node
                      //in the list

    while (current != NULL && !found)    //search the list
        if (current->info.checkTitle(title))  //the item is found
            found = true;
        else
            current = current->link;  //advance current to
                                      //the next node
}//end searchVideoList
```

如果搜索成功，参数 `found` 被设置为 `true`，并且参数 `current` 指向包含该视频信息的节点。如果搜索不成功，`found` 被设置为 `false`，并且 `current` 将为 `NULL`。

`class videoListType` 的其他函数定义如下：

```cpp
bool videoListType::isVideoAvailable(string title) const
{
    bool found;
    nodeType<videoType> *location;

    searchVideoList(title, found, location);

    if (found)
        found = (location->info.getNoOfCopiesInStock() > 0);
    else
        found = false;

    return found;
}

void videoListType::videoCheckIn(string title)
{
    bool found = false;
    nodeType<videoType> *location;

    searchVideoList(title, found, location); //Search the list

    if (found)
        location->info.checkIn();
    else
        cout << "The store does not carry " << title
             << endl;
}

void videoListType::videoCheckOut(string title)
{
    bool found = false;
    nodeType<videoType> *location;

    searchVideoList(title, found, location); //Search the list

    if (found)
        location->info.checkOut();
    else
        cout << "The store does not carry " << title
             << endl;
}

bool videoListType::videoCheckTitle(string title) const
{
    bool found = false;
    nodeType<videoType> *location;

    searchVideoList(title, found, location); //search the list

    return found;
}

void videoListType::videoUpdateInStock(string title, int num)
{
    bool found = false;
    nodeType<videoType> *location;

    searchVideoList(title, found, location); //search the list

    if (found)
        location->info.updateInStock(num);
    else
        cout << "The store does not carry " << title
             << endl;
}

void videoListType::videoSetCopiesInStock(string title, int num)
{
    bool found = false;
    nodeType<videoType> *location;

    searchVideoList(title, found, location);

    if (found)
        location->info.setCopiesInStock(num);
    else
        cout << "The store does not carry " << title
             << endl;
}

bool videoListType::videoSearch(string title) const
{
    bool found = false;
    nodeType<videoType> *location;

    searchVideoList(title, found, location);

    return found;
}
```
