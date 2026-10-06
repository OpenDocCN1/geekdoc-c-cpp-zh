# Example 2.12: The initialization and use of a structure variable.

```
// 2_12.cpp
#include <iostream>
#include <iomanip>
using namespace std;
    //structure of student information
{
    int num;              //student number
    char name[20];        //name
    char sex;              //sex
    int age;               //age
}stu={97001,"Lin Lin","F',19};

int main()
{
    cout<<setw(7)<<stu.num<<setw(20)<<stu.name<<setw(3)<<stu.sex
    <<setw(3)<<stu.age;

}
```

Result:

97001 Lin Lin F 19

The type of data can also construct a structure. The structure animal in Example 2.13 is made up of two int-type members.

Example 2.13: There are three animals and all of them have two attributes: weight and height. Now we need to assign their weights and heights, and then output their weights.

Analysis: these three animals have a weight and height attribute; therefore we declare a structure that includes the two attribute members (weight and height).

Source code:

```
// 2_13.cpp
#include <iostream>
using namespace std;
struct animal
{
    int weight;
    int feet;
};
```