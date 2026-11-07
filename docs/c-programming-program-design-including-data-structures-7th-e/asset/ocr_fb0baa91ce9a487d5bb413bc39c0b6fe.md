```
~~~cpp
cout << "Line 29: After inserting 444, "
     << "intDeq: ";                         //Line 29
copy(intDeq.begin(), intDeq.end(), screen);  //Line 30
cout << endl;                                //Line 31

intDeq.assign(2, 45);                        //Line 32

cout << "Line 33: After assigning two "
     << "copies of 45, intDeq: ";            //Line 33
copy(intDeq.begin(), intDeq.end(), screen);  //Line 34
cout << endl;                                //Line 35

intDeq.push_front(-10);                      //Line 36
intDeq.push_back(-999);                      //Line 37

cout << "Line 38: After inserting two "
     << "elements, one at the front " << endl
     << "       and one at the back, intDeq: "; //Line 38
copy(intDeq.begin(), intDeq.end(), screen);  //Line 39
cout << endl;                                //Line 40

return 0;
}
~~~
```

# **Sample Run:**

```
~~~text
Line 7: intDeq: 13 75 28 35
Line 12: After adding two more elements, one at the front
         and one at the back, intDeq: 0 13 75 28 35 100
Line 17: After removing the first two elements,
         intDeq: 75 28 35 100
Line 22: After removing the last two elements,
         intDeq = 75 28
Line 29: After inserting 444, intDeq: 75 444 28
Line 33: After assigning two copies of 45, intDeq: 45 45
Line 38: After inserting two elements, one at the front
         and one at the back, intDeq: -10 45 45 -999
~~~
```

The statement in Line 1 declares a deque container intDeq of type int; that is, all of the elements of intDeq are of type int. The statement in Line 2 declares screen to be an ostream iterator initialized to the standard output device. The statements in Lines 3 through 6 use the push_back operation to insert four numbers—13, 75, 28, and 35— into intDeq. The statement in Line 8 outputs the elements of intDeq. In the output, see the line marked Line 7, which contains the output of the statements in Lines 7 through 9.

The statement in Line 10 inserts 0 at the beginning of intDeq; the statement in Line 11 inserts 100 at the end of intDeq. The statement in Line 13 outputs the modified intDeq.

The statements in Lines 15 and 16 use the function pop_front to remove the first two elements of intDeq; the statement in Line 18 outputs the modified intDeq. The