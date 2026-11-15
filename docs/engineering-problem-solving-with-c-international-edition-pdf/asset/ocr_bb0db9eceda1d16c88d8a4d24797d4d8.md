![](bbox=[0.226, 0.093, 0.555, 0.413])

# Figure 4.6 Counter-controlled loop.

keyboard and stored in a counter: The counter is then used to control the number of iterations of the input loop. A flowchart of this looping structure is given in Figure 4.6.

This loop is easily implemented using a while loop or a for loop. We use a for loop in the following example to calculate the average of a set of exam scores entered from the keyboard:

```
/*.........................................................*/
/* Program chapter4_6                                    */
/* This programs finds the average of a set of exam scores. */
#include<iostream>//Required for cin, cout
using namespace std;

int main()
{
  // Declare and initialize objects.
  double exam_score, sum(0), average;
  int counter;

  // Prompt user for input.
  cout << "Enter the number of exam scores to be read ";
  cin >> counter;
  cout << "Enter " << counter << " exam scores separated "
       << " by whitespace ";
// Input exam scores using counter-controlled loop.
for(int i=1; i<=counter; ++i)
```