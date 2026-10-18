# DISPLAY 12.2 Implementation File for DigitalTime (part 3 of 3)

```
90     {
91         cout<< "Error illegal input to readMinute\n";
92         exit(1);
93     }
94
95     theMinute = (digitToInt(c1) * 10) + digitToInt(c2);
96
97     if (theMinute< 0 || theMinute> 59)
98     {
99         cout<< "Error illegal input to readMinute\n";
100        exit(1);
101     }
102 }
103
104 //Uses iostream, cctype, and cstdlib:
105 void readHour(istream& ins, int& theHour)
106 {
107     char c1, c2;
108     ins >> c1 >> c2;
109     if ( ! ( isdigit(c1) && (isdigit(c2) || c2 == ':' ) ) )
110     {
111         cout<< "Error illegal input to readHour\n";
112         exit(1);
113     }
114
115     if (isdigit(c1) && c2 == ':')
116     {
117         theHour = digitToInt(c1);
118     }
119     else//(isdigit(c1) && isdigit(c2))
120     {
121         theHour = (digitToInt(c1) * 10) + digitToInt(c2);
122         ins >> c2;//discard ':'
123         if (c2 != ':')
124         {
125             cout<< "Error illegal input to readHour\n";
126             exit(1);
127         }
128     }
129     if (theHour < 0 || theHour > 23)
130     {
131         cout<< "Error illegal input to readHour\n";
132         exit(1);
133     }
134 }
```