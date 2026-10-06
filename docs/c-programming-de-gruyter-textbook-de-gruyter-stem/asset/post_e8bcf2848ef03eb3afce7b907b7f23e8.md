
## 3 — 3 Functions

Source code:

```cpp
//3_2.cpp
#include <iostream>
using namespace std;
double power (double x, int n);

int main()
{
    int i;
    int value = 0;
    char ch;

    cout << "Enter an 8 bit binary number ";
    for (i = 7; i >= 0; i--)
    {
        cin >> ch;
        if (ch == '1')
            value += int(power(2,i));
    }
    cout <<"Decimal value is "<<value<<endl;\n}
}

double power (double x, int n)
{
    double val = 1.0;
    while (n--)
        val *= x;
    return(val);
}
```

Running result:

| Enter an 8 bit binary number 01101001 |
| Decimal value is 105 |

**Example 3.3:** Write a program to compute the value of $\pi$ using the following formula.

$\pi = 16 \arctan\left(\frac{1}{5}\right) - 4 \arctan\left(\frac{1}{239}\right)$

Use the following series to calculate the arctangent of a number:

Continue accumulating until the absolute value of one item in the series is less than $10^{-15}$. The type of $\pi$ and x are both double.

$\arctan(x) = x - \frac{x^3}{3} + \frac{x^5}{5} - \frac{x^7}{7} + \dots$

Source code:

```cpp
// 3_3.cpp
#include<iostream>
using namespace std;
int main()
{
    double a, b;
    double arctan(double x);
    a=16.0*arctan(1/5.0);
    b=4.0*arctan(1/239.0);
    //Note: Since the division of integers is to be rounded off, the
    // value of 1/5 and 1/239 are both 0.
    cout<<"PI="<<a-b<<endl;
}
double arctan(double x)
{
    int i;
    double r, e, f, sqr;
    sqr=x*x;
    r=0;
    e=x;
    i=1;
    while(e/i>1e-15)
    {
        f=e/i;
        r=(i%4==1) ? r+f : r-f;
        e=e*sqr;
        i+=2;
    }
    return r;
}
```

Running result:

![](img/5618306d085ac1bac8275d6c4c5bbf2a_100_0.png)

Example 3.4: Find the number $m$ between 11 and 999 where $m, m^2$, and $m^3$ are all palindromes, and then output $m$.

Palindromes are numbers that have symmetrical digits. For example: 121, 676, and 94249 are all palindromes. One instance that satisfies this subject's requirement is: $m=11, m^2=121, m^3=1331$.

Analysis: To check whether a number is a palindrome or not, we can get every digit of the number by continuously dividing it by 10 and obtaining the remainders. After getting all the digits, we reverse the digit order to get a new number, and compare the new number with the original. The original number is a palindrome if and only it is the same as the new number.

Source code:

```cpp
//3_4.cpp
#include <iostream>
using namespace std;
int main() {
    bool symm(long n) {
        long m;
        for(m=11;m<1000;m++)
            if (symm(m)&&symm(m*m)&&symm(m*m*m))
                cout<<"m="<<m<<" m*m="<<m*m<<" m*m="<<m*m*m<<endl;
    }
    bool symm(long n) {
        long i, m;
        i=n; m=0;
        while(i) {
            m=m*10+i%10;
            i=i/10;
        }
        return (m==n);
    }
    return 0;
}
```

Running result:

| m=11 | m*m=121 | m*m*m=1331 |
| m=101 | m*m=10201 | m*m*m=1030301 |
| m=111 | m*m=12321 | m*m*m=1367631 |

## 3.1 Definition and Use of Function

**Example 3.5:** Compute the value of the following formula and output the result.

$k = \begin{cases} \sin(r) + \sin(s) & \text{when } r^2 \le s^2 \\ \sin(r \times s) & \text{when } r^2 > s^2 \end{cases}$

Here the values of $r$ and $s$ are input from the keyboard. The approximate value of $\sin x$ is calculated using formula:

$$\sin x = \frac{x^3}{3!} - \frac{x^5}{5!} + \frac{x^7}{7!} - \dots = \sum (-1)^{n-1} \frac{x^{2n-1}}{(2n-1)!}$$

The precision of the calculation is $10^{-6}$. Stop accumulating until the absolute value of one item is less than the precision, and the accumulated value is the approximate value of $\sin x$.

Source code:

```cpp
//3_5.cpp
#include <iostream>
#include <cmath> //Header file math has declaration of mathematic functions
using namespace std;
int main()
{
    double k,r,s;
    double tsin(double x);
    cout<<"r=";
    cin>>r;
    cout<<"s=";
    cin>>s;
    if (r*r<=s*s)
        k=tsin(r)+tsin(s);
    else
        k=tsin(r*s);
    cout<<k<<endl;
}

double tsin(double x)
{
    double p=0.000001,g=0, t=x;
    int n=1;
    do {
        g=g+t;
        n++;
        t=-t*x/(2*n-1)/(2*n-2);
    } while(fabs(t)>=p);
    return g;
}
```

Running result:

```
r=5
s=8
1.37781
```

Example 3.6: Game of casting dice.
Game rules: Dice has six faces — counting by points they are 1, 2, 3, 4, 5, and 6. The player inputs an unsigned integer, and the seed is what is used to generate a random number at the beginning of the program.

In each turn the dice is cast twice, and we can get the total number of points. In the first turn, if the total number of points is 7 or 11, the player wins and the game is over; if the point is 2, 3, 12, the player loses and the game is over; otherwise the player records the total point as his. In the following turns, if the total number is equal to the player's point, the player wins and the game is over; if the point total is 7, the player loses and the game is over; otherwise it goes to the next round.

The function rolldice to simulate rolling the dice, getting the total point, and outputting it.

> Note: The system function rand(void) generates a pseudorandom number. The pseudorandom number is not really random. When we call this function continuously in a program it will generate a sequence of random numbers, we discover that it will generate the same sequence each time we run the program. This sequence is called a pseudorandom number sequence. It is because rand needs an initial seed called "seed", and different seeds will generate different sequences. Thus, if we give the program a different seed in each run, continuously calling rand will generate a different random number sequence. If the seed is not set, rand will use the default value 1 as the seed. Note that the method for setting the seed is somewhat special: it is not through the parameters of rand, but by calling another function srand(unsigned int seed) to set the seed before calling rand, and the parameter seed in the function rand is the seed of rand.

Source code:

```cpp
//3_6.cpp
#include <iostream>
#include <cstdlib>
using namespace std;
int rolldice(void);
int main()
{
    int gamestatus,sum,mypoint;
    unsigned seed;
    cout<<"Please enter an unsigned integer:";
    cin>>seed; //Input the seed for the random number
    rand(seed); //Pass the seed to rand()
    sum=rolldice(); //The first round, roll the dice and get the
    switch(sum)
    {
        case 7:
        case 11:
            gamestatus=1; //Win if total number of points is 7 or 11
            break;
        case 2:
        case 3:
        case 12:
            gamestatus=2; //Lose if the point is 2, 3, 12
            break;
        default:
            mypoint=sum; //Record the total point as his
            break;
    }
    while(gamestatus==0)
    {
        sum=rolldice();
        if(sum==mypoint)
        {
            gamestatus=1; //Win if total number is equal to player's point
        }
        else if(sum==7)
        {
            gamestatus=2; //Lose if point total is 7
        }
        // Otherwise it goes to the next round
    }
    if(gamestatus==1)
        cout<<"player wins"<<endl;
    else if(gamestatus==2)
        cout<<"player loses"<<endl;
    return 0;
}

int rolldice(void)
{
    int die1,die2,worksum;
    die1=1+rand()%6;
    die2=1+rand()%6;
    worksum=die1+die2;
    cout<<"player rolled "<<die1<<"++"<<die2<<'='<<worksum<<endl;
    return worksum;
}
```
