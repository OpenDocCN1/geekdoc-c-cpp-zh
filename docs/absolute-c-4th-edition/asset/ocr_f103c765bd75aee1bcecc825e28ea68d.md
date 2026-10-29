# Display 11.9  Hiding the Helping Functions in a Namespace (Implementation File) (part 2 of 3)

```
```cpp
25             exit(1);
26         }

27         theMinute = digitToInt(c1)*10 + digitToInt(c2);

28         if (theMinute < 0 || theMinute > 59)
29         {
30             cout << "Error: illegal input to readMinute\n";
31             exit(1);
32         }
33     }

34
35     //Uses iostream, cctype, and cstdlib:
36     void readHour(int& theHour)
37     {
38         char c1, c2;
39         cin >> c1 >> c2;
40         if ( (!isdigit(c1) && (isdigit(c2) || c2 == ':')) > )
41         {
42             cout << "Error: illegal input to readHour\n";
43             exit(1);
44         }

45         if (isdigit(c1) && c2 == ':')
46         {
47             theHour = digitToInt(c1);
48         }
49         else //(isdigit(c1) && isdigit(c2))
50         {
51             theHour = digitToInt(c1)*10 + digitToInt(c2);
52             cin >> c2; //discard ':'
53             if (c2 != ':')
54             {
55                 cout << "Error: illegal input to readHour\n";
56                 exit(1);
57             }
58         }

59         if (theHour == 24)
60             theHour = 0; //Standardize midnight as 0:00.

61         if ( theHour < 0 || theHour > 23 )
62         {
```
```