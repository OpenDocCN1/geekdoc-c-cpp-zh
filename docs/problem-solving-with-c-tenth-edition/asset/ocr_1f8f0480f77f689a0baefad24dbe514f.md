Dear Instructor [Instructor Name],

I am sorry that I am unable to turn in my homework at this time. First, I ate a rotten [Food], which made me turn [Color] and extremely ill. I came down with a fever of [Number 100-120]. Next, my [Adjective] pet [Animal] must have smelled the remains of the [Food] on my homework, because he ate it. I am currently rewriting my homework and hope you will accept it late.

Sincerely,
[Your Name]

5. The following is a short program that computes the volume of a sphere given the radius. It will compile and run, but it does not adhere to the program style recommended in Section 2.5. Rewrite the program using the style described in the chapter for indentation, adding comments, and appropriately named constants.

```
#include <iostream>
using namespace std;
int main()
{
    double radius, vm;
    cout << "Enter radius of a sphere." << endl; cin >> radius;
    vm = (4.0 / 3.0) * 3.1415 * radius * radius * radius;
    cout << " The volume is " << vm << endl;
    return 0;
}
```

# PROGRAMMING PROJECTS

Programming Projects require more problem-solving than Practice Programs and can usually be solved many different ways. Visit www.myprogramminglab.com to complete many of these Programming Projects online and get instant feedback.

+   1. A government research lab has concluded that an artificial sweetener commonly used in diet soda pop will cause death in laboratory mice. A friend of yours is desperate to lose weight but cannot give up soda pop. Your friend wants to know how much diet soda pop it is possible to drink without dying as a result. Write a program to supply the answer. The input to the program is the amount of artificial sweetener needed to kill a mouse (use 5 grams), the mass of the mouse (use 35 grams), and the weight of the dieter (use 45400 grams for a 100 pound person). Assume that the lethal dose for a mouse is proportional to the lethal dose for the human. A single can of soda pop has a mass of 350 grams. To ensure the safety of your friend, be sure the program requests the weight at which the dieter will stop dieting, rather than the dieter’s current weight. Assume that diet