(continued)

```
//determine whether the file was opened
if (inFile.is_open())
{
    //read store 1's sales amount
    inFile >> store1Sales;
    inFile.ignore();

    while (!inFile.eof())
{
        //read store 2's sales amount
        inFile >> store2Sales;
        inFile.ignore();

        //accumulate each store's sales amount
        storeTotal += store1Sales;
        storeTotal += store2Sales;

        //read store 1's sales amount
        inFile >> store1Sales;
        inFile.ignore();
    } //end file
    //close the file
    inFile.close();

    //display the total sales amount for each store
    cout << "Store 1's total sales: "
    cout << storeTotal << endl;
    cout << "Store 2's total sales: "
    cout << storeTotal << endl;
}
else
    cout << "File could not be opened." << endl;
//end if
sysystem("pause");
return 0;
}//end of main function
```

Figure 14-22 Code for Lab 14-4

![](bbox=[0.119, 0.737, 0.568, 0.843])

Figure 14-23 Contents of the Lab14.txt sequential access file