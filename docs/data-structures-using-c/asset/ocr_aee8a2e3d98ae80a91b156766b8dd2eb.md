```
cout << "\n Enter itemcode to be searched";
cin >> searchitcode;
indexfile.open("index.dat", ios::in);
while(!indexfile.eof())
{
    indexfile.read((char*)&index, sizeof(indexrec));
    if(index.itemcode == searchitcode && index.flag
== 1)
    {
        found = 1;
        break;
    }
}
if(found == 1)
{
    itemfile.open("item.dat", ios::in);
    /*Take the position from index file and go to
    that record in item file */
    itemfile.seekg((index.position) * sizeof(item));
    itemfile.read((char*)&item, sizeof(item));
    cout << "\n Item Record is";
    cout << "\nItemcode \t Item name \t Cost";
    cout << item.itemcode << item.itemname <<
item.cost;
    itemfile.close();
}
else
    cout << "\n Record not found";
    indexfile.close();
}
/* Delete a record */
void deleterecord()
{
    int searchitcode;
    struct indexrec index;
    fstream indexfile;
    long position,found = 0, c;
    cout << "\n Enter itemcode to be deleted";
    cin >> searchitcode;
    indexfile.open("Index.dat", ios::in | ios::out |
ios::app);
    c = 0;
    while(!indexfile.eof())
```