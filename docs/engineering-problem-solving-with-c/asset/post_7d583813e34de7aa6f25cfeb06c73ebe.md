
Our flowchart provides enough detail to develop our problem solution.

```
/*-------------------------------------------*/
/* Program chapter7_13 */
/* This program runs a simulation to calculate */
/* the probability of drawing 2 red cards, each */
/* with a face value less than 10, from a */
/* shuffled deck of 52 cards. The results are */
/* then compared to analytical results. */
#include<iostream> //Required for cout.
#include "Card.h" //Required for Card.
#include "CardDeck.h" //Required for CardDeck.
using namespace std;

int main()
{
 //Declare objects.
 CardDeck theDeck;
 Card card1, card2;
 double pE, eventCounter = 0;
 int n;
 bool isRed;

 cout << "Enter the analytical result ";
 cin >> pE;
 cout << "Enter number of experiments to run ";
 cin >> n;

 for(int i=0; i<n; ++i)
 {
 theDeck.shuffleDeck();
 card1 = theDeck.draw();
 card2 = theDeck.draw();

 //Check if the event occurred.
 if ( (card1.getSuit() == 'H' || card1.getSuit() == 'D')
 && (card2.getSuit() == 'H' || card2.getSuit() == 'D'))
 {
 isRed = true;
 }
 else
 {
 isRed = false;
 }
 if( isRed && (card1.getRank() < 10 && card2.getRank() < 10) )
 {
 ++eventCounter;
 cout << "Event " << eventCounter << endl;
 card1.displayCard(cout);
 cout << " ";
 card2.displayCard(cout);
 cout << endl;
 }//End if
 }//End for
 cout << "Analytical results: " << pE << endl
 << "Simulated results: " << eventCounter << '/' << n
 << " = " << eventCounter/n << endl;
 return 0;
 }
/*--------------------------------------------------------------*/
```

## 5. TESTING

We will test our solution twice with a small number of experiments so that we can look at the outcomes to ensure that we are counting the events correctly.

### Simulation 1

```
Enter the analytical result 0.0904977
Enter number of experiments to run 97
Event 1
4 of Diamonds 8 of Diamonds
Event 2
5 of Diamonds 2 of Hearts
Event 3
3 of Hearts 2 of Hearts
Event 4
4 of Diamonds 7 of Hearts
Event 5
7 of Hearts 8 of Hearts
Event 6
5 of Hearts 2 of Diamonds
Event 7
8 of Diamonds 4 of Hearts
Event 8
9 of Hearts 8 of Diamonds
Event 9
4 of Diamonds 9 of Hearts
Analytical results: 0.0904977
Simulated results: 9/97 = 0.0927835
```

### Simulation 2

```
Enter the analytical result 0.0904977
Enter number of experiments to run 97
Event 1
6 of Hearts 4 of Hearts
Event 2
8 of Hearts 5 of Hearts
Event 3
8 of Diamonds 2 of Hearts
Event 4
6 of Hearts 5 of Diamonds
Event 5
3 of Diamonds 8 of Hearts
Event 6
4 of Diamonds 3 of Hearts
Event 7
3 of Hearts 4 of Hearts
Analytical results: 0.0904977
Simulated results: 7/97 = 0.0721649
```

To run our simulation for larger values of n, we will comment out the print statements to speed up execution.

### Simulation 3

```
Enter the analytical result 0.0904977
Enter number of experiments to run 101371
Analytical results: 0.0904977
Simulated results: 9171/101371 = 0.0904697
```

### Simulation 4

```
Enter the analytical result 0.0904977
Enter number of experiments to run 101371
Analytical results: 0.0904977
Simulated results: 9101/101371 = 0.0897791
```

### Simulation 5

```
Enter the analytical result 0.0904977
Enter number of experiments to run 1111111
Analytical results: 0.0904977
Simulated results: 100368/1111111 = 0.0903312
```

### Modify 7.11

The following exercises require modification of program chapter7_13, however, no modification of Card or CardDeck is required.

- 1. Modify program chapter7_13 to calculate the probability of drawing 2 face cards.
- 2. Modify program chapter7_13 to calculate the probability of drawing 5 black cards.
- 3. Modify program chapter7_13 to calculate the probability of drawing 4 Aces.

## SUMMARY

### Key Terms

- alphanumeric character
- null character
- string class
- array
- offset
- subscripts
- binary search
- one-dimensional array
- Unified Modeling Language (UML)
- event space
- sample space
- variance
- C-style string
- selection sort algorithm
- vector class
- character string
- sequential search
- whitespace
- magnitude
- sorting
- zero crossing
- mean
- standard deviation
- median
- statistical measurements

### C++ Statement Summary

```
Include C-style string header file
#include<cstring>
Include string class header file
#include<string>
Include vector class header file
#include<vector>
Range-based for Statement
for(declaration:range)
statement;
Array and vector declaration:
int a[5], b[]={2, 3, -1};
char vowels[]={'a', 'e', 'i', 'o', 'u'};
string words[100];
vector<double> time;
```

### Notes

- 1. The identifier i is commonly used as a subscript for a one-dimensional array.
- 2. Use symbolic constants to declare the size of an array so that it is easy to modify.

### Notes

- 1. Use arrays only when it is necessary to keep all the data available in memory.
- 2. If unexpected characters are printed at the end of a C-style string, the null character may be missing from the string.
- 3. Be careful not to exceed the maximum offset value when referencing an element in an array.
- 4. An array must be declared to be as large as, or larger than, the maximum number of values to be stored in it.
- 5. Because an array reference in a function is always a pass by reference, be careful that you do not inadvertently change values in an array in the function.

## Problems

### Exam Practice!

#### True/False Problems

Indicate whether the following statements are true (T) or false (F).

- 1. If the initializing sequence is shorter than an array, then the rest of the values are initialized to zero. T F
- 2. If an array is defined without a size, but with an initialization sequence, then the array size is arbitrary. T F
- 3. When the value of a subscript or offset is greater than the largest valid offset of an array, it will always cause an execution error. T F
- 4. All values of an array are printed if we specify the identifier of the array without an offset. T F
- 5. In ASCII, the string "Smith" is less than the string "Johnson". T F

#### Multiple-Choice Problems

- 6. An array is
- (a) a group of values having a common object name and all of the same data type.
- (b) a collection of elements of different data types which are stored in adjacent memory locations.
- (c) an object that contains multiple values of the same data type.
- (d) a location in memory that holds multiple values of the same data type.
- 7. An individual element in an array is addressed by specifying
- (a) the name of the array and the offset of the element.
- (b) the name of the array.
- (c) the offset of the element within the array followed by the name of the array.
- (d) the offset of the element in the array.
- 8. The offset identifies the __________ of a particular element in the array.
- (a) location
- (b) value
- (c) range
- (d) name

#### Memory Snapshot Problems

Give the corresponding snapshots of memory after each of the following sets of statements is executed. Use ? to indicate an array element that is not initialized.

```
9. int t[5];
...
t[0] = 5;
for (int k=0; k<4; k++)
t[k+1] = t[k] + 3;
10. char s[] = "Hello", t[] = {'a', 'e', 'i', 'o', 'u'}, name[10];
strcpy(name, "Sue");
```

### Program Output

Problems 11-13 refer to the following statements:

```
string strng1 = "k", strng2 = "265", strng3 = "xyz";
```

- 11. What is the output of the following statement?

```
cout << strng1.size() << endl;
```

- 12. What is the output of the following statement?

```
strng1 = strng2;
cout << strng1 << endl;
```

- 13. What is the output of the following statements?

```
strng1 += strng2;
cout << strng1 << endl;
```

Problems 14-16 refer to the following statements:

```
double x[] = { 2, 4, 6, 8, 10, 12 }, sum = 0;
```

- 14. What is the output of the following statements?

```
for (double k : x)
{
   cout << k << " ";
}
```

- 15. What is the output of the following statements?

```
for (double k : x)
   sum += k;
cout << sum << endl;
```

- 16. What is the output of the following statements?

```
for (double k : x)
{
   cout << k << " ";
   --k;
   cout << k << endl;
}
```

## Programming Exercises

### Linear Interpolation.

The following problems refer to the wind-tunnel test data stored in the file tunnel.dat. The file contains the set of data which consists of a flight-path angle (in degrees) and its corresponding coefficient of lift on each line in the file. The flight-path angles will be in ascending order.

- 17. Write a program that reads the wind-tunnel test data and then allows the user to enter a flight-path angle. If the angle is within the bounds of the data set, the program should then use linear interpolation to compute the corresponding coefficient of lift. (You may need to refer to the section on linear modeling in Section 5.6.)
