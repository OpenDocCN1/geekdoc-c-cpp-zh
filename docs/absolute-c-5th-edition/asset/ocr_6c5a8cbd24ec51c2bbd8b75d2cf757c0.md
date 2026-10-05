# 254 CHAPTER 6 Structures and Classes

Display 6.3 Class with a Member Function (part 2 of 3)

```
33      else
34          cout << "Happy Unbirthday!\n";
35          return 0;
36  }
37  //Uses iostream; <-- Member function definition
38  void DayOfYear::output( )
39  {
40      switch (month)
41          {
42              case 1: cout << "January \ break;
43              case 2: cout << "February"; break;
44              case 3: cout << "March"; break;
45              case 4: cout << "April"; break;
46              case 5: cout << "May"; break;
47              case 6: cout << "June"; break;
48              case 7: cout << "July"; break;
49              case 8: cout << "August"; break;
50              case 9: cout << "September"; break;
51              case 10: cout << "October"; break;
52              case 11: cout << "November"; break;
53              case 12: cout << "December"; break;
54              default:
55                  cout << "Error in DayOfYear::output.";
56          }
n57      cout << day;
58  }
```