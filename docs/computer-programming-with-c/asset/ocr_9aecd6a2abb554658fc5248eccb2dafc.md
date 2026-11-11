```
```cpp
b[books_issued].input();
books_issued++;
}
}
void return_book()
{
int id,i;
cout<<"Enter the book ID of the book to be returned"<<endl;
cin>>id;
/*we set the ID of the book as -1 once the book is returned*/
for(i=0;i<books_issued;i++)
{
    if(b[i].getId()==id)
    {
        b[i].setId(-1);
        books_issued--;
        return;
    }
}
cout<<"The Book with ID"<<id<<"is not issued by the
customer"<<endl;
}
void output()
{
cout<<"the ID name and tel_no of the customer is"<<endl;
cout<<customer_id<<"  "<<cname<<"  "<<tel_no<<endl;
cout<<"The number of books issued by the customer
are:"<<books_issued<<endl;
    int i;
    for(i=0;i<books_issued;i++)
    {
        if(b[i].getId()!=-1)
        {
            b[i].output();
        }
    }
}
};
void main()
{
Customer c1,c2;
```
```