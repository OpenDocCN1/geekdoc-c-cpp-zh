

以下步骤描述了该算法：

- 1. 将搜索项与链表中的当前节点进行比较。如果当前节点的信息大于或等于搜索项，则停止搜索；否则，将下一个节点设为当前节点。
- 2. 重复步骤1，直到找到链表中大于或等于搜索项的项，或者链表中没有更多数据可与搜索项比较为止。

请注意，该循环并未显式检查搜索项是否等于链表中的某个项。因此，循环执行后，我们必须检查搜索项是否等于链表中的项。

```cpp
template <class Type>
bool orderedLinkedList<Type>::
    search(const Type& searchItem) const
{
    bool found = false;
    nodeType<Type> *current; //pointer to traverse the list

    current = first;  //start the search at the first node

    while (current != NULL && !found)
        if (current->info >= searchItem)
            found = true;
        else
            current = current->link;

    if (found)
        found = (current->info == searchItem); //test for equality

    return found;
}//end search
```

### 插入节点

要在有序链表中插入一个项，我们首先找到新项应插入的位置，然后将该项插入链表。为了找到新项的位置，和之前一样，我们搜索链表。这里我们使用两个指针 current 和 trailCurrent 来搜索链表。指针 current 指向其信息正与待插入项进行比较的节点，trailCurrent 指向 current 之前的节点。由于链表有序，搜索算法与之前相同。会出现以下情况：

**情况1：** 链表初始为空。包含新项的节点是唯一节点，因此是链表中的第一个节点。

**情况2：** 新项小于链表中的最小项。新项放在链表开头。在这种情况下，我们需要调整链表的头指针——即 first。同时，count 增加1。

**情况3：** 该项要插入到链表中的某个位置。

## 德比郡：一家历史悠久、坚韧不拔的足球俱乐部

德比郡足球俱乐部位于英格兰德比，是世界上历史最悠久、最具传奇色彩的足球俱乐部之一。该俱乐部成立于1884年，拥有超过140年的丰富传统，以卓越成就、令人难忘的球员和热情的球迷群体为标志。

俱乐部最伟大的时代出现在20世纪70年代布莱恩·克拉夫执教时期。克拉夫与助手彼得·泰勒一起，带领德比郡于1972年首次夺得甲级联赛冠军，并于1975年再次夺冠。这一时期巩固了德比郡作为英格兰足球一支强大力量的地位。

多年来，德比郡经历了足球命运的全貌——从在棒球场征战欧洲赛场的荣耀，到降级和财务动荡的心碎。尽管面临挑战，俱乐部的精神从未动摇，这在很大程度上要归功于忠实的支持者。

- **成立时间：** 1884
- **球场：** 普莱德公园球场（容量33,597）
- **昵称：** 公羊队
- **球队颜色：** 白色和黑色
- **竞争对手：** 诺丁汉森林、莱斯特城

德比郡还以其卓越的青训学院而闻名，该学院培养了许多顶级球员，他们后来在国内和国际赛场上大放异彩。这种培养年轻人才的承诺仍然是俱乐部理念的基石。

> “德比郡不仅仅是一家足球俱乐部；它是一种生活方式，是一种根深蒂固的激情，将一代代球迷紧密相连。”

近年来，俱乐部在普莱德公园球场进行比赛，这是一座于1997年启用的现代化场馆。该球场举办了许多令人难忘的比赛，其氛围在足球联赛中广受赞誉。普莱德公园不仅仅是一座球场——它是一座堡垒，梦想和回忆在这里铸就。

随着德比郡继续它的旅程，历史的回响和球迷坚定不移的支持提供了恒久的基础。从克拉夫的辉煌岁月到现代，公羊队自豪地屹立，准备迎接接下来的一切。

**情况3b：** 待插入项位于链表中间某处。考虑图18-35所示的链表。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1103_0.png)

假设我们要在此链表中插入27。显然，27位于17和38之间，这需要修改信息为17的节点的链接。插入27后，得到的链表如图18-36所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1103_1.png)

根据情况3，我们必须首先遍历链表以找到新项要插入的位置。由此还可知，我们应该使用两个指针——例如 current 和 trailCurrent——遍历链表。指针 current 用于遍历链表，并将链表中节点的信息与待插入项进行比较。指针 trailCurrent 指向 current 之前的节点。例如，在情况3b中，当搜索停止时，trailCurrent 指向节点17，current 指向节点38。该项插入在 trailCurrent 之后。在情况3a中，搜索链表找到65的位置后，trailCurrent 指向节点54，current 为 NULL。

本质上，函数 insert 如下所示：

```cpp
template <class Type>
void orderedLinkedList<Type>::insert(const Type& newItem)
{
    nodeType<Type> *current; //pointer to traverse the list
    nodeType<Type> *trailCurrent; //pointer just before current
    nodeType<Type> *newNode; //pointer to create a node
    bool found;

    newNode = new nodeType<Type>; //create the node
    newNode->info = newItem;       //store newItem in the node
    newNode->link = NULL;          //set the link field of the node
                                  //to NULL

    if (first == NULL)   //Case 1
    {
        first = newNode;
        last = newNode;
        count++;
    }
    else
    {
        current = first;
        found = false;

        while (current != NULL && !found) //search the list
            if (current->info >= newItem)
                found = true;
            else
            {
                trailCurrent = current;
                current = current->link;
            }

        if (current == first)      //Case 2
        {
            newNode->link = first;
            first = newNode;
            count++;
        }
        else                       //Case 3
        {
            trailCurrent->link = newNode;
            newNode->link = current;

            if (current == NULL)
                last = newNode;

            count++;
        }
    }//end else
}//end insert
```

### 插入首节点与插入尾节点

函数 insertFirst 将新项插入到链表开头。然而，由于结果链表必须保持有序，新项必须插入到适当位置。类似地，函数 insertLast 必须将新项插入到适当位置。

```cpp
if (first == NULL)  //Case 1
    cout << "Cannot delete from an empty list." << endl;
else
{
    current = first;
    found = false;

    while (current != NULL && !found)  //search the list
        if (current->info >= deleteItem)
            found = true;
        else
        {
            trailCurrent = current;
            current = current->link;
        }

    if (current == NULL)  //Case 4
        cout << "The item to be deleted is not in the "
             << "list." << endl;
    else
        if (current->info == deleteItem) //the item to be
                                         //deleted is in the list
        {
            if (first == current)       //Case 2
            {
                first = first->link;

                if (first == NULL)
                    last = NULL;

                delete current;
            }
            else                        //Case 3
            {
                trailCurrent->link = current->link;

                if (current == last)
                    last = trailCurrent;

                delete current;
            }
            count--;
        }
        else                            //Case 4
            cout << "The item to be deleted is not in the "
                 << "list." << endl;
}
} //end deleteNode
```

### 有序链表的头文件

为了完整性，我们将展示如何创建定义 `class orderedListType` 的头文件，以及此类链表上的操作。（我们假设

