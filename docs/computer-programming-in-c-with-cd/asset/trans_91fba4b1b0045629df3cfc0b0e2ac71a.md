
```cpp
rational operator-(rational); //The operator - will perform the
                             // subtraction operation for two
                             // rational numbers

rational operator*(rational); //The operator * will perform the
                             // multiplication operation for two
                             // rational numbers

rational operator/(rational); //The operator / will perform the division
                             // operation for two
                             // rational numbers

void operator+=(rational);    //Overloading the operator for assignment
                             // addition functions
void operator-=(rational);    //Overloading the operator for assignment
                             // subtraction functions
void operator*=(rational);    //Overloading the operator for assignment
                             // multiplication functions
void operator/=(rational);    //Overloading the operator for assignment
                             // division functions
};
int zero=0;

rational::rational(void) //The function constructor which will be overloaded
                         // with 2 parameters somewhere later in the program
{
    num=0;
    den=0;
}

rational::rational(int n, int d) //As mentioned earlier, the overloaded
                                 // function with 2 parameters, where the entered
                                 // values will form the numerator and the
                                 // denominator of the fraction respectively
{
    num=n;
    den=d;
}

void rational::display(void) //Function to display the fraction
{
    cout<<num<<endl<<"--"<<endl<<den;
}
rational rational::operator +(rational r2)
{
    int n,d;
    n=num*r2.den+r2.num*den; //Adding two fractions using the cross
                             // multiplication technique

    d=den*r2.den;
    return rational(n,d);
}

rational rational::operator -(rational r2)
{
    int n,d;
    n=num*r2.den-r2.num*den; //Subtracting two fractions using the cross
                             // multiplication technique

    d=den*r2.den;
    return rational(n,d);
}

rational rational::operator *(rational r2)
{
    int n,d;
    n=num*r2.num; //Multiplying two fractions
    d=den*r2.den;
    return rational(n,d);
}

rational rational::operator /(rational r2)
{
    int n,d;
    n=num*r2.den; //Dividing two fractions
    d=den*r2.num;
    return rational(n,d);
}
void rational::operator +=(rational r)
{
    num=num*r.den+r.num*den;
    den=den*r.den;
}
void rational::operator -=(rational r)
{
    num=num*r.den-r.num*den;
    den=den*r.den;
}
void rational::operator *=(rational r)
{
    num=num*r.num;
    den=den*r.den;
}
void rational::operator /=(rational r)
{
    if(r.num)
    {
        num*=r.den;
        den*=r.num;
    }
    else //Maintaining a check for division by zero
    {
        zero=1;
        cout<<endl<<"Division by zero!!!(numerator in the second rational number is a 0)";
        cout<<endl<<"Press any key to exit to main menu";
        getch();
    }
}
//function main begins
void main()
{
    int choice,flag;
    int n,d,n1,d1;
    rational temp;
    char cont;

    clrscr();
    cout<<"Enter numerator for a : ";
    cin>>n;
    do
    {
        cout<<"Enter denominator for a : ";
        cin>>d;
    }while(d==0);

    cout<<"Enter numerator for b : ";
    cin>>n1;
    do
    {
        cout<<"Enter denominator for b : ";
        cin>>d1;
    }while(d1==0);

    rational r1(n,d);
    rational r2(n1,d1);
    do
    {
        clrscr();
        flag=0,zero=0;
        cout<<"OPERATIONS ON RATIONAL NUMBERS";
        cout<<endl<<"1.Addition";
        cout<<endl<<"2.Subtraction";
        cout<<endl<<"3.Multiplication";
        cout<<endl<<"4.Division";
        cout<<endl<<"5.Assignment addition(+=)";
        cout<<endl<<"6.Assignment subtraction(-=)";
        cout<<endl<<"7.Assignment multiplication(*)";
        cout<<endl<<"8.Assignment division(/=)";
        cout<<endl<<"9.Exit";

        do //Implementing a switch case structure for exercising the options
        {
            cout<<endl<<"Enter choice(1-10) : ";
            cin>>choice;
        }while(choice<=0 || choice>9);

        switch(choice)
        {
            case 1:
                temp=r1+r2;
                temp.display();
                break;

            case 2:
                temp=r1-r2;
                temp.display();
                break;

            case 3:
                temp=r1*r2;
                temp.display();
                break;

            case 4:
                temp=r1/r2;
                temp.display();
                break;

            case 5:
                r1+=r2;
                r1.display();
                break;

            case 6:
                r1-=r2;
                r1.display();
                break;

            case 7:
                r1*=r2;
                r1.display();
                break;

            case 8:
                r1/=r2;
                if (!zero)
                    r1.display();
                break;

            case 9:
                exit(0);
                break;
        };

        cout<<endl<<"Continue(y/n) ? : ";
        cin>>cont;
        if(toupper(cont)=='Y')
            flag=1;
    }while(flag==1);
    getch();
}
```

## Q42：实现一个使用链表将两个多项式相加的程序，以便结果同时显示系数和指数。

答：

```cpp
#include<iostream.h>
#include<conio.h>
#include<ctype.h>
#include<math.h>

class term //declaring a class of the name Term
{
    public: //All the terms below this declaration are public
        int coeff,pow; //The node class will have data fields containing
                       // the coefficient and power of each of the terms of
                       // the polynomial.
        term *link; //The link field will point to the next node
        void input() //The input function for the class
        {
            cout<<"\n\nEnter coefficient : ";
            cin>>coeff;
            cout<<"\nEnter exponent   : ";
            cin>>pow;
            cout<<endl;
        }
        void output() //The output function for the class
        {
            if(coeff<0)
                cout<<" - ";
            else
                cout<<" + ";
            cout<<abs(coeff);
            cout<<"x^"; //Preparing the output format to determine how the
                        // output should look like
            cout<<pow;
        }
};
class pol //Creating a linked list containing all the terms of the polynomial
{
    public:
        term *head;
        void create();
        void display();
        void add(pol *,pol *);
};
void main()
{
    pol p;
    clrscr();
    p.create(); //Creating the polynomial linked list
    cout<<endl;
    p.display(); //Displaying the polynomial linked list
    getch();
}
void pol::create()
{
    term *ptr,*p;
    cout<<"\n\nEnter terms in decreasing order of exponent please.\n\n";
    p=new term; //creating a new node and later on declaring it as a head to
                // determine where the linked list begins from
    head=p;
    do
    {
        ptr=p;
        p->input();
        p=new term;
        ptr->link=p;
        ptr=p;
        cout<<"Want to enter another term? (y/n)";
    }while(toupper(getche())!='N'); //Continue the process until the user enters 'n' to
                                    // the process of wanting to enter another term
    p->link=NULL; //once the user has entered n, the last node after that should be
                  // pointing to NULL since there are no nodes after that
}
void pol::display() //Function to display the output
{
    term *ptr=head; //Starting to read from the head of the list
    while(ptr!=NULL) //Until the pointer reaches the NULL pointer, continue to print
                     // the output
    {
        ptr->output();
        ptr=ptr->link;
    }
}
void pol::add(pol *A,pol *B)
{
    term *ptr=new term,*p1=A->head,*p2=B->head; //The new pointer p will hold the
                                                // of the coefficients
    if(p1->pow>p2->pow) //Determining which of the two polynomials have a larger
                        // power to determine where to begin the addition of the
                        // coefficients from
    {
        ptr->coeff=p1->coeff; //In case the first polynomial has a larger coefficient
                               // we have to begin counting from here, so storing that
                               // value in the pointer coefficient field
        ptr->pow=p1->pow;
        p1=p1->link;
    }
    else if(p2->pow>p1->pow)
    {
        ptr->coeff=p2->coeff; //In case the second polynomial has a larger
                              // coefficient, we have to begin counting from here, so
                              // storing that value in the pointer coefficient field
        ptr->pow=p2->pow;
        p2=p2->link;
    }
    else //In case both the polynomials have the same power, begin addition of the
         // coefficients of the two polynomials straightaway
    {
        ptr->coeff=p1->coeff+p2->coeff;
        ptr->pow=p1->pow;
        p1=p1->link;
        p2=p2->link;
    }
    head=ptr;
    while((p1!=NULL) && (p2!=NULL))
    {
        p=new term;
        if(p1->pow>p2->pow)
        {
            p->coeff=p1->coeff;
            p->pow=p1->pow;
```
