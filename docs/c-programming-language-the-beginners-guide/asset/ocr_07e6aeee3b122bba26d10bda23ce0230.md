```
1 #include 2
3 int main()
4 {

• struct person {
• char name[32];
• int age;

8 };

• struct person president = {

• "George Washington",

11 67
12 };
13
14 printf("%s was %d years old\n",president.name,president.age);
15
16 return(o);
17 }
18
19
```

In this code, a structure named *person* is declared. A variable of the person type is declared at line 9. It is named The president structure variable is immediately assigned with values. The values match the structure member types and are enclosed in curly brackets. Run this code to ensure that it works.

One thing to note in the structure is how you assign a string to a structure member. Take a look at the code below: