```
```cpp
void marklist::pop()
{
    int no;
    no=head->data.rollno;
    head=head->link;
    cout<<"\nrecord with roll no "<<no<<" has been deleted";
    display();
}

void main()
{
    clrscr();
    marklist m1;
    int ch;
    char ans='Y';
    do
    {
        cout<<"\n1.Input\n2.Insert\n3.delete\n4.Push\n5.Pop\n6.Sort\nEnter ur
        choice:";
        cin>>ch;
        switch(ch)
        {
            case 1:
                m1.input();
                break;
            case 2:
                m1.insert();
                break;

            case 3:
                m1.del();
                break;

            case 4:
                m1.push();
                break;

            case 5:
                m1.pop();
                break;
            case 6:
                m1.sort();
                break;
            default:
```
```