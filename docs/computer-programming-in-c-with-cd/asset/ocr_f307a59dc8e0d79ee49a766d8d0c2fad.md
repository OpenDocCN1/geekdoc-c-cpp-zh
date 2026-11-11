```
```
}
}
void main()
{
int x,y,x1,y1,choice,flag,c,temp;
clrscr();
cout<<"enter the no of rows and columns of the first matrix: ";
cin>>x>>y;
matrix m1(x,y);
m1.input();
m1.display();
cout<<"\nenter the no of rows and columns of the second matrix: ";
cin>>x1>>y1;
matrix m2(x1,y1);
m2.input();
m2.display();
cout<<"\nwhat do you want to do with the two matrices ?";
cout<<"\nenter 1 for addition , 2 for multiplication ,3 for transpose";
cout<<"\nenter your choice  ";
matrix m3(x,y1);
cin>>choice;
switch(choice) //A switch structure is used to enhance user friendliness
{ case 1: //This case is for matrix addition
{
if((x1!=x)||(y1!=y)) //If the number of rows and columns are not the same
 then the
                         // matrices cannot be added.
{
cout<<"\nthese two matrices cannot be added";
break;
}
} else
m3.calculation(m1,m2);
m3.display();
break;
}
case 2: //If the number of rows of the first array, is not equal to the
number of
                 //columns of the second array then the multiplication cannot be
done
{
if(y!=x1)
{
```
```