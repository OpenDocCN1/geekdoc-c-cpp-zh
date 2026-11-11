```
```
int main()
{
    Student object1;
    object1.inputData();
    object1.displayData();
    return 0;
}
```
```

**Output:**

```
```text
Enter student's roll number
1001
Enter student's name
Kabir
Enter student's age
12
Enter student's class
7
Enter subject code
104
Enter marks scored by student
87
Student's Roll Number:1001
Student's Name:Kabir
Student's Age:12
Student's Class:7
Subject Code:104
Student's Marks:87
```
```

In Listing 2, the Student class has the declaration of two member functions, `inputData()` and `displayData()`. The declaration of a function, without definition, is also called the prototype of a function. The return type of the `inputData()` and `displayData()` functions is `void`. The `inputData()` function is defined outside the boundary of the class Student using the scope resolution operator (`::`). Consider the following code snippet:

```
```
void Student::inputData()
{
...
...
...
}
```
```

In the preceding code snippet, `void` is the return type of the `inputData()` function. Student is the name of the user-defined class followed by scope resolution operator (`::`), and `inputData()` is the name of a function declared in the Student class. The `inputData()` function is defined outside the boundary of the Student class to accept the information, such as, roll number, name, and marks of any student.