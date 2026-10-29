
through `finalIndex`. The two extra parameters will specify the first and last indexes of the search, so we will call them `first` and `last`. Using these parameters for the lowest and highest indexes, instead of 0 and `finalIndex`, we can express the pseudocode more precisely, as follows:

```
To search a[first] through a[last] do the following:
    found = false; //so far.
    mid = approximate midpoint between first and last;
    if (key == a[mid])
    {
        found = true;
        location = mid;
    }
    else if (key < a[mid])
        search a[first] through a[mid - 1];
    else if (key > a[mid])
        search a[mid + 1] through a[last];
```

To search the entire array, the algorithm would be executed with `first` set equal to 0 and `last` set equal to `finalIndex`. The recursive calls will use other values for `first` and `last`. For example, the first recursive call set `first` equal to 0 and `last` equal to the calculated value `mid - 1`.

As with any recursive algorithm, we must ensure that our algorithm ends rather than producing infinite recursion. If the sought-after number is found on the list, then there is no recursive call and the process terminates, but we need some way to detect when the number is not on the list. On each recursive call the value of `first` is increased or the value of `last` is decreased. If they ever pass each other and `first` and `last` are equal or become larger than `last`, we will know that there are no more indexes left to check and that the number key is not in the array. If we add this test to our pseudocode, we obtain a complete solution, as shown in Display 13.6.

## Coding

Now we can routinely translate the pseudocode into C++ code. The result is shown in Display 13.7. The function `search` is an implementation of the recursive algorithm given in Display 13.6. A diagram of how the function performs on a sample array is given in Display 13.8.

Notice that the function `search` solves a more general problem than the original task. Our goal was to design a function to search an entire array, yet the search function will let us search any interval of the array by specifying the index bounds `first` and `last`. This is common when designing recursive functions. Frequently, it is necessary to solve a more general problem in order to be able to express the recursive algorithm. In this instance, we wanted only the answer in the case where `first` and `last` are set equal to 0 and `finalIndex`. However, the recursive calls will set them to values other than 0 and `finalIndex`.

## Display 13.7 Recursive Function for Binary Search (part 2 of 2)

This portion of the program contains some code to fill and sort the array a. The exact details are irrelevant to this example.

```
16  int key, location;
17  bool found;
18  cout << "Enter number to be located: ";
19  cin >> key;
20  search(a, 0, finalIndex, key, found, location);

21  if (found)
22      cout << key << " is in index location "
23          << location << endl;
24  else
25      cout << key << " is not in the array." << endl;

26  return 0;
27 }
28 void search(const int a[], int first, int last,
29             int key, bool& found, int& location)
30 {
31     int mid;
32     if (first > last)
33     {
34         found = false;
35     }
36     else
37     {
38         mid = (first + last)/2;
39
40         if (key == a[mid])
41         {
42             found = true;
43             location = mid;
44         }
45         else if (key < a[mid])
46         {
47             search(a, first, mid - 1, key, found, location);
48         }
49         else if (key > a[mid])
50         {
51             search(a, mid + 1, last, key, found, location);
52         }
53     }
}
```

## Display 13.8 Execution of the function search

key is 63

54 a[0] 15
55 a[1] 20
56 a[2] 35
57 a[3] 41
58 a[4] 57
59 a[5] 63
60 a[6] 75
61 a[7] 80
62 a[8] 85
63 a[9] 90

first == 0

mid = (0 + 9)/2

last == 9

54 a[0] 15
55 a[1] 20
56 a[2] 35
57 a[3] 41
58 a[4] 57
59 a[5] 63
60 a[6] 75
61 a[7] 80
62 a[8] 85
63 a[9] 90

Not in this half

first == 5

mid = (5 + 9)/2

last == 9

next

54 a[0] 15
55 a[1] 20
56 a[2] 35
57 a[3] 41
58 a[4] 57
59 a[5] 63
60 a[6] 75
61 a[7] 80
62 a[8] 85
63 a[9] 90

first == 5

last == 6

Not here

next

mid = (5 + 6)/2 which is 5
a[mid] is a[5] == 63
found = TRUE;
location = mid;

## Checking the Recursion

The subsection entitled “Recursive Design Techniques” gave three criteria that you should check to ensure that a recursive void function definition is correct. Let’s check these three things for the function search given in Display 13.7.

- 1. There is no infinite recursion: On each recursive call the value of first is increased or the value of last is decreased. If the chain of recursive calls does not end in some other way, then eventually the function will be called with first larger than last, which is a stopping case.

- 2. Each stopping case performs the correct action for that case. There are two stopping cases, when first > last and when key == a[mid]. Let’s consider each case.
  - If first > last, there are no array elements between a[first] and a[last] so key is not in this segment of the array. (Nothing is in this segment of the array!) So, if first > last, the function search correctly sets found equal to false.
  - If key == a[mid], the algorithm correctly sets found equal to true and location equal to mid. Thus, both stopping cases are correct.

- 3. For each of the cases that involve recursion, if all recursive calls perform their actions correctly, then the entire case performs correctly. There are two cases in which there are recursive calls, when key < a[mid] and when key > a[mid]. We need to check each of these two cases.

First, suppose key < a[mid]. In this case, since the array is sorted, we know that if key is anywhere in the array, then key is one of the elements a[first] through a[mid - 1]. Thus, the function needs only to search these elements, which is exactly what the recursive call

```
search(a, first, mid - 1, key, found, location);
```

does. So if the recursive call is correct, then the entire action is correct.

Next, suppose key > a[mid]. In this case, since the array is sorted, we know that if key is anywhere in the array, then key is one of the elements a[mid + 1] through a[last]. Thus, the function needs only to search these elements, which is exactly what the recursive call

```
search(a, mid + 1, last, key, found, location);
```

does. So if the recursive call is correct, then the entire action is correct. Thus, in both cases the function performs the correct action (assuming that the recursive calls perform the correct action).

The function search passes all three of our tests, so it is a good recursive function definition.

## Efficiency

The binary search algorithm is extremely fast compared with an algorithm that simply tries all array elements in order. In the binary search, you eliminate about half the array

from consideration right at the start. You then eliminate a quarter, then an eighth of the array, and so forth. These savings add up to a dramatically fast algorithm. For an array of 100 elements, the binary search will never need to compare more than 7 array elements to the key. A simple serial search could compare as many as 100 array elements to the key, and on the average will compare about 50 array elements to the key. Moreover, the larger the array is, the more dramatic the savings will be. On an array with 1000 elements, the binary search will need only to compare about 10 array elements to the key value, as compared to an average of 500 for the simple serial search algorithm.

An iterative version of the function search is given in Display 13.9. On some systems the iterative version will run more efficiently than the recursive version. The algorithm for the iterative version was derived by mirroring the recursive version. In the iterative version, the local variables first and last mirror the roles of the parameters in the recursive version, which are also named first and last. As this example illustrates, it often makes sense to derive a recursive algorithm even if you expect to later convert it to an iterative algorithm.

## Display 13.9 Iterative Version of Binary Search (part 1 of 2)

### Function Declaration

```
void search(const int a[ ], int lowEnd, int highEnd,
    int key, bool& found, int& location);
//Precondition: a[lowEnd] through a[highEnd] are sorted in
//increasing order.
//Postcondition: If key is not one of the values a[lowEnd]
//through a[highEnd], then found == false; otherwise,
//a[location] == key and found == true.
```

### Function Definition

```
void search(const int a[ ], int lowEnd, int highEnd,
    int key, bool& found, int& location)
{
    int first = lowEnd;
    int last = highEnd;
    int mid;

    found = false;//so far
    while ((first <= last) && !(found))
    {
        mid = (first + last)/2;
        if (key == a[mid])
        {
            found = true;
            location = mid;
```

(continued)
