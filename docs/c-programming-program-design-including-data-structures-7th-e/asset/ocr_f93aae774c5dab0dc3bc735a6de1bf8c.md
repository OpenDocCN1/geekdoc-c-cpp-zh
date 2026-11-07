```
```cpp
cout << "Line 8: Number of Zs in charList = "
     << noOfZs << endl;                         //Line 8
//count_if
int noOfUpper = count_if(charList.begin(),
                         charList.end(), isupper); //Line 9

cout << "Line 10: Number of uppercase letters"
     << " in charList = " << noOfUpper << endl; //Line 10

int list[10] = {12, 34, 56, 21, 34,
                78, 34, 55, 12, 25};           //Line 11

ostream_iterator<int> screenOut(cout, " ");     //Line 12

cout << "Line 13: list: ";                       //Line 13
copy(list, list + 10, screenOut);                //Line 14
cout << endl;                                    //Line 15

//max_element
int *maxLoc = max_element(list, list + 10);      //Line 16
cout << "Line 17: Largest element in list = "
     << *maxLoc << endl;                         //Line 17

//min_element
int *minLoc = min_element(list, list + 10);      //Line 18

cout << "Line 19: Smallest element in list = "
     << *minLoc << endl;                         //Line 19

//random_shuffle
random_shuffle(list, list + 10);                  //Line 20

cout << "Line 21: list after random shuffle:\n"
     << "     ";                                //Line 21
copy(list, list + 10, screenOut);                //Line 22
cout << endl;                                    //Line 23

return 0;
}
void doubleNum(int num)
{
    cout << 2 * num << " ";
}
```
```

# Sample Run:

Line 4: charList: Z a Z B Z C D e F Z  
Line 8: Number of Zs in charList = 4  
Line 10: Number of uppercase letters in charList = 7  
Line 13: list: 12 34 56 21 34 78 34 55 12 25