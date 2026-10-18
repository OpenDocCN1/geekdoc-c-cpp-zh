
## DISPLAY 14.5 Pseudocode for Binary Search

```
int a[Some_Size_Value];
```

Algorithm to search a[first] through a[last]

```
1    //Precondition:
2    //a[first]<= a[first + 1] <= a[first + 2] <= ... <= a[last]
```

To locate the value key:

```
1    if (first > last) //A stopping case
2        found = false;
3    else
4    {
5        mid = approximate midpoint between first and last;
6        if (key == a[mid]) //A stopping case
7        {
8            found = true;
9            location = mid;
10       }
11       else if key < a[mid] //A case with recursion
12           search a[first] through a[mid - 1];
13       else if key > a[mid] //A case with recursion
14           search a[mid + 1] through a[last];
15   }
```

## DISPLAY 14.6 Recursive Function for Binary Search (part 1 of 2)

```
1    //Program to demonstrate the recursive function for binary search.
2    #include <iostream>
3    using namespace std;
4    const int ARRAY_SIZE = 10;
5
6
7    void search(const int a[], int first, int last,
8        int key, bool& found, int& location);
9    //Precondition: a[first] through a[last] are sorted in increasing order.
10   //Postcondition: if key is not one of the values a[first] through a[last],
11   //then found == false; otherwise, a[location] == key and found == true.
12
13
14   int main()
15   {
16       int a[ARRAY_SIZE];
17       const int finalIndex = ARRAY_SIZE - 1;
```

(continued)

## DISPLAY 14.6 Recursive Function for Binary Search (part 2 of 2)

< This portion of the program contains some code to fill and sort the array a. The exact details are irrelevant to this example. >

```
19    int key, location;
20    bool found;
21    cout << "Enter number to be located: ";
22    cin >> key;
23    search(a, 0, finalIndex, key, found, location);
24
25    if (found)
26        cout << key << " is in index location "
27           << location << endl;
28    else
29        cout << key << " is not in the array." << endl;
30
31    return 0;
32 }
33 void search(const int a[], int first, int last,
34                int key, bool& found, int& location)
35 {
36    int mid;
37    if (first > last)
38    {
39        found = false;
40    }
41    else
42    {
43        mid = (first + last)/2;
44
45        if (key == a[mid])
46        {
47            found = true;
48            location = mid;
49        }
50        else if (key < a[mid])
51        {
52            search(a, first, mid -1, key, found, location);
53        }
54        else if (key > a[mid])
55        {
56            search(a, mid + 1, last, key, found, location);
57        }
58    }
59 }
```

## DISPLAY 14.7 Execution of the Function search

key is 63

a[0] 15
 a[1] 20
 a[2] 35
 a[3] 41
 a[4] 57
 a[5] 63
 a[6] 75
 a[7] 80
 a[8] 85
 a[9] 90
 first == 0
 mid = (0 + 9)/2
 last == 9
 Next

a[0] 15
 a[1] 20
 a[2] 35 Not in this half
 a[3] 41
 a[4] 57
 a[5] 63 first == 5
 a[6] 75
 a[7] 80 mid = (5 + 9)/2
 a[8] 85
 a[9] 90 last == 9

a[0] 15
 a[1] 20
 a[2] 35
 a[3] 41
 a[4] 57
 a[5] 63 first == 5
 a[6] 75 last == 6
 a[7] 80
 a[8] 85
 a[9] 90
 Not here
 Next

mid = (5 + 6)/2 which is 5
 a[mid] is a[5] == 63
 found = true;
 location = mid;

## Solve a more general problem

Notice that the function search solves a more general problem than the original task. Our goal was to design a function to search an entire array. Yet the function will let us search any interval of the array by specifying the index bounds first and last. This is common when designing recursive functions. Frequently, it is necessary to solve a more general problem in order to be able to express the recursive algorithm. In this case, we only wanted the answer in the case where first and last are set equal to 0 and finalIndex. However, the recursive calls will set them to values other than 0 and finalIndex.

## Checking the Recursion

In the subsection entitled “Recursive Design Techniques,” we gave three criteria that you should check to ensure that a recursive void function definition is correct. Let’s check these three things for the function search given in Display 14.6.

- 1. There is no infinite recursion: On each recursive call, the value of first is increased or the value of last is decreased. If the chain of recursive calls does not end in some other way, then eventually the function will be called with first larger than last, and that is a stopping case.

- 2. Each stopping case performs the correct action for that case: There are two stopping cases: when first > last and when key==a[mid]. Let’s consider each case.
  
  If first > last, there are no array elements between a[first] and a[last], and so key is not in this segment of the array. (Nothing is in this segment of the array!) So, if first > last, the function search correctly sets found equal to false.
  
  If key==a[mid], the algorithm correctly sets found equal to true and location equal to mid. Thus, both stopping cases are correct.

- 3. For each of the cases that involve recursion, if all recursive calls perform their actions correctly, then the entire case performs correctly: There are two cases in which there are recursive calls: when key < a[mid] and when key > a[mid]. We need to check each of these two cases.

First suppose key < a[mid]. In this case, since the array is sorted, we know that if key is anywhere in the array, then key is one of the elements a[first] through a[mid-1]. Thus, the function need only search these elements, which is exactly what the recursive call

```
search(a, first, mid - 1, key, found, location);
```

does. So if the recursive call is correct, then the entire action is correct.

Next, suppose key > a[mid]. In this case, since the array is sorted, we know that if key is anywhere in the array, then key is one of the elements a[mid+1] through a[last]. Thus, the function need search only these elements, which is exactly what the recursive call

```
search(a, mid + 1, last, key, found, location);
```

does. So if the recursive call is correct, then the entire action is correct. Thus, in both cases the function performs the correct action (assuming that the recursive calls perform the correct action).

The function search passes all three of our tests, so it is a good recursive function definition.

## Efficiency

The binary search algorithm is extremely fast compared to an algorithm that simply tries all array elements in order. In the binary search, you eliminate about half the array from consideration right at the start. You then eliminate a quarter, then an eighth of the array, and so forth. These savings add up to a dramatically fast algorithm. For an array of 100 elements, the binary search will never need to compare more than 7 array elements to the key. A simple serial search could compare as many as 100 array elements to the key and on the average will compare about 50 array elements to the key. Moreover, the larger the array is, the more dramatic the savings will be. On an array with 1000 elements, the binary search will need to compare only about 10 array elements to the key value, as compared to an average of 500 for the simple serial search algorithm.

An iterative version of the function search is given in Display 14.8. On some systems, the iterative version will run more efficiently than the recursive version. The algorithm for the iterative version was derived by mirroring the recursive version. In the iterative version, the local variables first and last mirror the roles of the parameters in the recursive version, which are also named first and last. As this example illustrates, it often makes sense to derive a recursive algorithm even if you expect to later convert it to an iterative algorithm.

Iterative version

## DISPLAY 14.8 Iterative Version of Binary Search (part 1 of 2)

### Function Declaration

```
1   void search(const int a[], int lowEnd, int highEnd,
2   int key, bool& found, int& location);
3   //Precondition: a[lowEnd] through a[highEnd] are sorted in increasing
4   //order.
5   //Postcondition: If key is not one of the values a[lowEnd] through
6   //a[highEnd], then found == false; otherwise, a[location] == key and
7   //found == true.
```

### Function Definition

```
1   void search(const int a[], int lowEnd, int highEnd,
2     int key, bool& found, int& location)
3   {
4     int first = lowEnd;
5     int last = highEnd;
```

(continued)
