```
/* The following for loop is not required. This will actually be added by the compiler when the array is defined by the class in the first line (Item ItemArray[]20;) by calling the Item() constructor. */
for(int i=0; i<20; i++)
    ItemArray[i].SetDetails(0, "");

// The following is important
ItemIndex = 0;
}

/* This default constructor is needed as ItemIndex is initialized here and afterwards incremented. Other parts of the constructor are redundant and can be removed. */

void PrintDetails()
{
    for(int i=0; i<ItemIndex; i++)
        ItemArray[i].ShowDetails();
}

void InsertItem(int TempItemNo, string TempItemName)
{
    ItemArray[ItemIndex].SetDetails(TempItemNo, TempItemName);
    ItemIndex++;
    /* This statement flags an error in the absence of a default constructor */
};
int main()
{
    ItemCollection IC;
    IC.InsertItem(105,"Pentium4 processor"); IC.InsertItem(111,"Seagate HDD");
    IC.InsertItem(122,"Samsung monitor"); IC.InsertItem(220,"Creative sound card");
    IC.PrintDetails();
}
```

# How the Program Works

Programs 5.1 and 5.2 have two different classes; one is Item and the other is ItemCollection, which contains an array of items. Both of them have default constructors defined. Let us ignore the default constructor for Item and consider only that for ItemCollection in the second case, because it is important here. Program 5.1 contains functions that insert values in the complete set of items in a single shot, using an array. Program 5.2 inserts items one by one. The default constructor in Program 5.1 initializes item numbers as zeros and names as blank strings and also initializes ItemIndex to zero. If this default constructor is removed, it will have no effect on the program, which would be executed as it is.

However, in Program 5.2, initializing ItemIndex to zero is an important step. If the default constructor is removed, the program will not be able to function properly because the functions InsertItem() and PrintDetails() are dependent on that value. Every time InsertItem() is called, ItemIndex is incremented. When the function is called for the first time, it has to increment from zero. If it is not initialized to zero, InsertItem() inserts items at random locations represented by the value of ItemIndex.

It is also possible to define constructors other then default constructors. Let us discuss this in detail.