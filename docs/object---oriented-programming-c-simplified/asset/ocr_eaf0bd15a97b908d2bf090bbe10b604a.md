# OUTPUT :

Enter no of elements <= 20
6
Enter 6 elements
60 10 30 20 45 25
Given array is
60 10 30 20 45 25
Sorted array is :
10 20 25 30 45 60

![](bbox=[0.25, 0.32, 0.75, 0.535])

Figure 15.33.Output screen of the program.

# Experiment-10 : Write programs illustrating file handling operations :

+   (a) Copying a text file
+   (b) Displaying the contents of the file, etc.

# /*PROGRAM : READING AND WRITING MOBILE DETAIL */

```
#include <iostream.h>
#include <fstream.h>
void main()
{
    fstream rw;
    rw.open("demo2.txt",ios ::out);
    char mcomp[20],model[10];
    float price;
    cout<<"Enter the mobile model"<<endl;
    cin.getline(model, 10);
    cout<<"Enter the mobile company"<<endl;
    cin.getline(mcomp, 20);
```