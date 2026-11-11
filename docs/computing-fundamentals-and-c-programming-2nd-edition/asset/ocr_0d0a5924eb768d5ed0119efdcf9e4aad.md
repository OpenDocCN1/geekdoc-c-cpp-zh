```
```c
fEdit=TRUE;
if(CheckId(code)==0)
{
    if(messagebox(0,33,"Press Enter key to edit the item.","Confirm",
                  mboxbrdrclr,mboxbgclr,mboxfgclr,0)!=13)
    {
        messagebox(10,33,"The item information could not be modified. Please try
        again.","Edit ",mboxbrdrclr,mboxbgclr,mboxfgclr,0);
        fEdit=FALSE;
        break;
    }
    fEdit=TRUE;
    getdata();
    fflush(stdin);
    fseek(dbfp,-stocksize,SEEK_CUR);
    fwrite(&inv_stock,stocksize,1,dbfp);
}
else
    messagebox(10,33,"The item is not available in the database.","No records found",
              mboxbrdrclr,mboxbgclr,mboxfgclr,0);
    fEdit=FALSE;
    break;

    /* To show information about an item*/
    case '3':
print2screen(2,33,"Enter Item Code: ",BROWN,BLUE,0);gotopos(2,55);fflush(stdin);
scanf("%s",&code);
flag=0;
rewind(dbfp);
while(fread(&inv_stock,stocksize,1,dbfp)==1)
{
    if(strcmp(inv_stock.itemcode,code)==0)
    {
        Displayiteminfo();
        flag=1;
    }
}
if(flag==0)
    messagebox(10,33,"The item is not available.","No records found ",
              mboxbrdrclr,mboxbgclr,mboxfgclr,0);
    break;

    /* To show information about all items in the database*/
```
```