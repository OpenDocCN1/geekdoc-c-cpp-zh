
```cpp
flag=0;
} //End of if block

if(ch1==ch2)
{
    flag=0;
    textcolor(WHITE);
    cprintf("%c",ch2);
}
else
{
    count++;
    flag++;
    textcolor(RED);
    cprintf("%c",ch2);
}
} //End of for block

textcolor(WHITE);
gotoxy(25,29);
cout<<setprecision(2);
cout<<"Speed - "<<(9*60)/difftime(t2,t1)<<" words per min";
gotoxy(25,31);
cout<<"Accuracy - "<<(float(noc-count)/float(noc))*100.00<<"% ";
fptr1.close();
fptr2.close();
while(1)
{
    gotoxy(25,34);
    cout<<"Practice Again? (Y/N)";
    ch1=getch();
    if(toupper(ch1)=='Y')
        break;
    else if(toupper(ch1)=='N')
```

```cpp
time_t t1;
time(&t1);

for(int i=0;i<405;i++)
{
    ch2=getche();
    fptr2.put(ch2);
}
time_t t2;
time(&t2);

fptr2.close();

fptr1.open("test.txt",ios::in);
fptr2.open("type2.txt",ios::in);

gotoxy(1,26);
printf("Typing Test Results...");

gotoxy(1,29);
int flag=0;
int flag2=0;
int flag3=0;
for(i=0;i<405;i++)
{
    fptr1.get(ch1);
    fptr2.get(ch2);
    if(flag==5)
    {
        while(1)
        {
            if(flag2==0)
                fptr1.get(ch1);
            if(flag3==0)
                fptr2.get(ch2);
            if(ch1==' ')
                flag2=1;
            if(ch2==' ')
                flag3=1;
            if(flag2==1 && flag3==1)
                break;
        }
        flag=0;
    }
    if(ch1==ch2)
    {
        flag=0;
        textcolor(WHITE);
        cprintf("%c",ch2);
    }
    else
    {
        count++;
        flag++;
        textcolor(RED);
        cprintf("%c",ch2);
    }
}
textcolor(WHITE);
gotoxy(1,37);

cout<<setprecision(2);
cout<<"Speed - "<<(71*60)/difftime(t2,t1)<<" words per min";

gotoxy(1,39);
cout<<"Accuracy - "<<(float(noc-count)/float(noc))*100.00<<"%";

fptr1.close();
fptr2.close();
while(1)
{
    gotoxy(1,42);
    cout<<"Take the test again? (Y/N)";
    ch1=getch();
    if(toupper(ch1)=='Y')
        break;
    else if(toupper(ch1)=='N')
        return;
}
} //End of test()
```

## Application Output

The following is a series of screenshots depicting how the Typing Tutor application functions.

![](img/62b7c32e48e4f960a8dc2825a7119fb2_732_0.png)

**Fig. A.1.** *The Main Screen*

![](img/62b7c32e48e4f960a8dc2825a7119fb2_733_0.png)

**Fig. A.2.** *The Typing Tips Screen*

![](img/62b7c32e48e4f960a8dc2825a7119fb2_733_1.png)

**Fig. A.3.** *The Typing Practice Screen*

![](img/62b7c32e48e4f960a8dc2825a7119fb2_734_0.png)

**Fig. A.4.** *The Typing Test Screen*

## A.2 Major Project: Telephone Billing System

### Learning Objectives

After going through this project work, you will be able to:

- Understand how command-driven applications are developed.
- Apply the concept of classes and objects to real world situations.
- Learn how file I/O operations are performed in C++.

### Telephone Billing System

Telephone Billing System is a command-driven application that helps manage records of the customers and generate their telephone bills. [Table A.2](#table-a-2) lists the various coding elements of the application:

**Table A.2.** *Key Coding Elements*

| Element | Description |
|---|---|
| account | The account class realises the real world entity customer. |
| obj | An instantiation of the account class, obj is primarily used to work with the data at hand and update it in the backend database file. |
| db.dat | Is the primary database file which stores all the backend data for the application. |
| add() | This class method adds a new customer record. |
| del() | This class method deletes an existing customer record. |
| modify() | This class method modifies an existing customer record. |
| display() | This class method displays a list of existing customer records. |
| generate() | This class method generates the bill for an existing customer record. |
| help() | This class method displays help documentation to the user. |
| numdigits() | This method returns the number of digits contained in the passed integer value. |
| mon() | This method converts a month's value from integer to string. |

```cpp
void generate();

void help();
};
account obj;

int bil_ctr=1; //Counter variable for bill id

/*Function for counting number of digits in an integer*/
int numdigits(long n)
{
    return(log10(n)+1);
}
/*Function for converting a month's value from integer to string*/
char *mon(int m)
{
    switch(m)
    {
        case(1):
            return("Jan");
        case(2):
            return("Feb");
        case(3):
            return("Mar");
        case(4):
            return("Apr");
        case(5):
            return("May");
        case(6):
            return("Jun");
        case(7):
            return("Jul");
        case(8):
            return("Aug");
        case(9):
            return("Sep");
        case(10):
```

```cpp
obj.add();
break;
case 'M':
    obj.modify();
    break;
case 'D':
    obj.del();
    break;
case 'E':
    break;
} //End of inner switch-case block
} while(ch2!='E'); //End of do-while block
} //End of outer switch-case block
} //End of while block
} //End of main()

/*Function for adding a new customer record*/
void account :: add()
{
    char ch1;
    fstream fptr1;
    fptr1.open("db.dat",ios::app);
    if(fptr1.fail())
    {
        cout<<"Cannot open the db.dat file!";
        getch();
        return;
    }
    clrscr();
    gotoxy(30,5);
    cout<<"Enter the new customer's details..";
    while(1)
    {
        gotoxy(30,8);
        cout<<"Name : ";
        gets(name);
        if(strlen(name)==0)
        {
            gotoxy(30,30);
            clreol();
            cout<<"Name cannot be left blank!";
        }
        else
        {
            gotoxy(30,30);
            clreol();
            break;
        }
    }
    while(1)
    {
        gotoxy(30,10);
        cout<<"Address : ";
        gets(address);
        if(strlen(address)==0)
        {
            gotoxy(30,30);
            clreol();
            cout<<"Address cannot be left blank";
        }
        else
        {
            gotoxy(30,30);
            clreol();
            break;
        }
    }
    while(1)
    {
        gotoxy(30,12);
        cout<<"Ph. No : ";
        cin>>phone_no;
        if(numdigits(phone_no)!=7)
        {
            gotoxy(54,12);
            clreol();
            gotoxy(30,30);
            clreol();
            cout<<"Phone no must be of seven digits";
        }
        else
        {
            gotoxy(30,30);
            clreol();
            break;
        }
    }
    while(1)
    {
        gotoxy(30,14);
        cout<<"Acc no : ";
        cin>>acc_no;
        if(numdigits(acc_no)!=5)
        {
            gotoxy(54,14);
            clreol();
            gotoxy(30,30);
            clreol();
            cout<<"Account no must be of five digits";
        }
        else
        {
            gotoxy(30,30);
            clreol();
            break;
        }
    }
    gotoxy(30,30);
    cout<<"'S'ave and Exit";
    gotoxy(30,32);
    cout<<"'E'xit without saving ";
    ch1=getch();
    ch1=toupper(ch1);

    switch(ch1)
    {
        case 'S':
            fptr1.write((char *)this,sizeof(obj));
            fptr1.close();
            return;
        case 'E':
            fptr1.close();
            return;
    }
} //End of add()

/*Function for modifying a customer record*/
void account :: modify()
{
    char ch;
    long input_no;
    int flag=0;
    fstream fptr1,fptr2;

    fptr1.open("db.dat",ios::in);
    if(fptr1.fail())
    {
        cout<<"Cannot open the db.dat file!";
        getch();
        return;
    }
    fptr2.open("dbtemp.dat",ios::out);
    if(fptr2.fail())
    {
        cout<<"Cannot open the dbtemp.dat file!";
        getch();
        return;
    }
    clrscr();
    gotoxy(20,3);
    cout<<"Enter the phone no whose record is to be modified: ";
    cin>>input_no;
    while(fptr1.read((char *)this, sizeof(obj)))
    {
        if(input_no==phone_no)
        {
            flag=1;
            gotoxy(20,5);
            cout<<"Name "<<name;
            gotoxy(20,6);
            cout<<"Address "<< address;
            gotoxy(20,7);
            cout<<"Acc No "<<acc_no;
            gotoxy(20,10);
            cout<<"Modify this customer record (Y/N) ";
            ch = getch();
            ch=toupper(ch);
            if(ch=='Y')
            {
                gotoxy(20,14);
                cout<<"Enter the customer's modified details.\n";
                while(1)
                {
                    gotoxy(20,16);
                    cout<<"Name : ";
                    gets(name);
                    if(strlen(name)==0)
                    {
                        gotoxy(30,30);
                        clreol();
                        cout<<"Name cannot be left blank!";
                    }
                    else
                    {
                        gotoxy(30,30);
                        clreol();
                        break;
                    }
                }

                while(1)
                {
                    gotoxy(20,18);
                    cout<<"Address : ";
                    gets(address);
                    if(strlen(address)==0)
                    {
                        gotoxy(30,30);
                        clreol();
                        cout<<"Address cannot be left blank";
                    }
                    else
                    {
                        gotoxy(30,30);
                        clreol();
                        break;
                    }
                }
                while(1)
                {
                    gotoxy(20,20);
                    cout<<"Ph. No : ";
                    cin>>phone_no;
                    if(numdigits(phone_no)!=7)
                    {
                        gotoxy(44,20);
```
