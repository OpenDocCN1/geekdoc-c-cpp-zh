```
ItemsInterested[i] = TempItemsInterested[i];
}
TotalItems = TempTotalItems;
}
void ShowDetails()
{
cout << "\n Customer number is " << CustNo;
cout << "\n Customer name is " << CustName;
cout << "\n Customer address is " << CustAddress;
cout << "\n" << CustName << "is interested in following items" << "\n";
for(int i=0; i<TotalItems; i++)
{
ItemsInterested[i].ShowDetails();
}
}
friend Item ModifyItem(customer & TempCust, int ItemNoToBeReplaced);
};
void main()
{
customer Steve;
Item ItemArray[]=
{
Item(3,"Sandwiches"), Item(4,"Paper Bags"),
Item(5,"Napkins"), Item(6,"Toys"), Item(10,"Biscuits"),
Item(9,"Pen"), Item(1,"Pencil"), Item(2,"Eraser"),
};
Steve = customer(2, "Steve Waugh", "Australia", ItemArray, 5);
customer Mark(Steve);
Steve.ShowDetails();
Mark.ShowDetails();
ModifyItem(Mark, 3);
Mark.ShowDetails();
Steve.ShowDetails();
// Without copy constructor, it would show the same result
}
/* The following function is using private variables of both the classes, so it is made friend of both */
Item ModifyItem(customer & TempCust, int ItemNoToBeReplaced)
{
for(int i=0; i<TempCust.TotalItems; ++i)
{
if(TempCust.ItemsInterested[i].ItemNo) == ItemNoToBeReplaced)
{
cout << "Enter new details for item to be replaced \n";
cout << "Enter item no. \n";
int TempItemNo;
cin >> TempItemNo;
cout << "Enter item name \n";
string TempItemName;
cin >> TempItemName;
```