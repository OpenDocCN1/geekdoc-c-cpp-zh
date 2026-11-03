The keyword *struct* is followed by the name of the structure. In this case, the name is The structure members are contained in curly brackets; each ending with a semi-colon because the whole deal is a statement. The structure members are variable declarations. Inside this structure, you’ll find an *int* and a *float* member. The *int* member is named The *float* member is named

By itself, the structured declaration merely creates a type of structure, like a new type of variable in the code. To use the structure, you need to declare a variable of the structure type. On line 9 we’re going to type the following:

```
1  #include 2
3  int main()
4  {

•  struct record {
•  int account;
•  float balance;

8  };
9  struct record my_bank; 10
11 return(0);
12 }
13
14
```