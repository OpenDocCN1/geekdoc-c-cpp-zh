The identity of an indexed variable, such as score[i], is determined by the value of its index, which in this instance is i. Thus, you can write programs that say things like "do such and such to the ith indexed variable," where the value of i is computed by the program. For example, the program in Display 5.1 reads in scores and processes them in the way described at the start of this chapter.

# Display 5.1 Program Using an Array

```
//Reads in five scores and shows how much each
//score differs from the highest score.
#include <iostream>
using namespace std;

int main()
{
    int i, score[5], max;
    cout << "Enter 5 scores:\n";
    cin >> score[0];
    max = score[0];
    for (i = 1; i < 5; i++)
    {
        cin >> score[i];
        if (score[i] > max)
            max = score[i];
        //max is the largest of the values score[0],..., score[i].
    }
    cout << "The highest score is " << max << endl
         << "The scores and their\n"
         << "differences from the highest are:\n";
    for (i = 0; i < 5; i++)
        cout << score[i] << " off by "
             << (max - score[i]) << endl;
    return 0;
}
```

# SAMPLE DIALOGUE

Enter 5 scores:
5 9 2 10 6
The highest score is 10
The scores and their
differences from the highest are:
5 off by 5
9 off by 1
2 off by 8
10 off by 0
6 off by 4