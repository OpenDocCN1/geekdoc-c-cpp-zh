# Display 11.2  Implementation File (part 3 of 3)

```
```cpp
83      exit(1);
84  }
85  theMinute = digitToInt(c1)*10 + digitToInt(c2);

86  if (theMinute < 0 || theMinute > 59)
87  {
88      cout << "Error: illegal input to readMinute\n";
89      exit(1);
90  }
91 }

92 //Uses iostream, cctype, and cstdlib;
93 void DigitalTime::readHour(int& theHour)
94 {
95     char c1, c2;
96     cin >> c1 >> c2;
97     if ( (!isdigit(c1) && (isdigit(c2) || c2 == ':')) )
98     {
99         cout << "Error: illegal input to readHour\n";
100        exit(1);
101    }
102
103    if (isdigit(c1) && c2 == ':')
104    {
105        theHour = DigitalTime::digitToInt(c1);
106    }
107    else //(isdigit(c1) && isdigit(c2))
108    {
109        theHour = DigitalTime::digitToInt(c1)*10
110                 + DigitalTime::digitToInt(c2);
111        cin >> c2; //discard ':'
112        if (c2 != ':')
113        {
114            cout << "Error: illegal input to readHour\n";
115            exit(1);
116        }
117    }

118    if (theHour == 24)
119        theHour = 0;  //Standardize midnight as 0:00

120    if ( theHour < 0 || theHour > 23 )
121    {
122        cout << "Error: illegal input to readHour\n";
123        exit(1);
124    }
125 }
```
```