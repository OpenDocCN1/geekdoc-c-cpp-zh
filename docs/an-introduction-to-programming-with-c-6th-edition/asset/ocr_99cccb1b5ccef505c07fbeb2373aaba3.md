displayAge function included in the original program, the modified program defines and calls a void function named getAge. The function call, which appears on Line 15, passes the age by reference. You can tell that the variable is by reference because the address-of-operator defines the formal parameter in the getAge function's header (Line 24) and in its prototype (Line 8). Note that the statement that calls a function does not indicate whether an item is passed by value or by reference. You can determine that information only by examining the parameterList in either the function's header or its prototype. The displayAge function, getAge is a void function; however, its call appears as a statement itself. Again, notice that the data type of the actual argument in the function call matches the type of the formal parameter listed in the function header and prototype. Also notice the name of the actual argument (age) is different from the name of the formal parameter (years).

```
1 //Modified Age.cpp - displays the user's age in a message
2 //Created/revised by <name> on <current date>
3
4 #include <iostream>
5 using std;
6
7 //function prototype
8 void getAge(int &years);
9 void displayAge(int &years);
10
11 int main()
12 {
13 int age = 0;
14 //get age
15 getAge(age);
16 //display age(age);
17 displayAge(age);
18
19 system("pause");
20 return 0;
21 } //end of main function
22
23 //****function definitions****n24 void getAge(int &years)
25 {
26 cout << "How old are you?";
27 cin >> years;
28 } //end of getAge function
29
30 void displayAge(int &years)
31 {
32 cout << "You are " << years << " years old." << endl;
33 } //end of displayAge function
```

![](bbox=[0.596, 0.447, 0.725, 0.467])

![](bbox=[0.731, 0.467, 0.859, 0.497])

![](bbox=[0.663, 0.693, 0.792, 0.713])

Figure 10-10 Modified age message program