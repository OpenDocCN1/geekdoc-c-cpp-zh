
```cpp
AS.MyArr[x] = 15;             //initializes the value of (x-1)th element to 15.
int newVar = AS.MyArr[x];  /*assigns the value of (x-1)th element to integer variable newVar*/
```

### Q9. How can you create an array of the structure in C++?

Ans. A structure is basically a user-defined data type that contains variables of various predefined data types. Similar to the arrays of other predefined data types, you can also create an array of the structure. In such a case, each array item represents all the elements of the structure. Suppose you have created a structure student by using the following code snippet:

```cpp
struct student
{
char name [25];
int age;
float marks;
};
```

Now, you need to store the information of 50 students. Therefore, you can create an array of the student structure by using the following code snippet:

```cpp
student class6 [50];
```

After declaring an array of the structure, each array item contains all the elements of the structure.

### Q10. How can you pass a pointer of the structure variable to the function as an argument and access members of the structure?

Ans. Passing a structure pointer to a function means that you are passing a pointer of the structure variable as an argument to a function. In this scenario, the address of the structure variable is passed as an argument by using the pointer (*) while defining a function. For this, you have to define a pointer variable of the structure in the C++ program. The syntax of defining pointer to structure is as follows:

```cpp
structure_name *structure_pointer_variable;
```

Where, *structure_pointer_variable is a pointer variable of the structure_name structure. Now, you can access the member elements of the structure by using the structure pointer variable and the arrow operator (->), as shown in the following syntax:

```cpp
structure_pointer_variable -> memberelement;
```

In the preceding code, you use the arrow operator (->) to access the member elements of the pointer structure variable.

### Q11. What is a linked list?

Ans. Linked list is a type of data structure that consists of the collection of elements in a linear manner. The basic idea behind a linked list is the inclusion of items that contain the pointer which points to the point in the list of the same data structure. For example, you have created a structure which consists of two data fields (quantity and price) and a pointer of the structure itself to contain the address of the next node. Such a type of structure declaration that has a chain of nodes where each node points to another node is known as a linked list.

### Q12. What is a union? How it is different from a structure?

Ans. A union is a user-defined data type that contains variables of various predefined data types. Unions are useful for those applications that involve multiple members and where the values need not be assigned to all the members at a time. The declaration of a union starts with the keyword union that is followed by a user-defined union name, and then curly braces. Within the body (between the opening and closing curly braces) of a union, you can define any number of members or variables of any data type, such as int, float.

Unlike structures, the members of a particular union can share the same storage area within the computer’s memory. This is why each instance of the structure occupies the memory equal to the sum of memory required to store all the elements defined in the structure. On the other hand, each instance of the union occupies only the memory in which the biggest element of the union can be stored.

# Debugging Exercises

### Q1. What will be the output of the following program?

```cpp
#include <iostream.h>
struct season
{
    char *name;
    int duration;
};
int main()
{
    season s1, s2;

    s1.name = "winter";
    s2.name = "Summer";

    s1.duration = 4;
    s2.duration = 8;

    cout<<"The season that lasts for "<<s1.duration<<" months is: "<<s1.name<<endl;
    cout<<"The season that lasts for "<<s2.duration<<" months is: "<<s2.name<<endl;

    return 0;
}
```

Ans. Output of the preceding program is as follows:

```text
The season that lasts for 4 months is: Winter
The season that lasts for 8 months is: Summer
```

### Q2. What will be the output of the following program?

```cpp
#include <iostream.h>
#include <stdio.h>
struct student
{
    char name[20];
    char AdmissionStatus[20];
    int FeesPaid;
    char stream[20];
};
int main()
{
    student s1;

    cout<<"Enter student name: ";
    gets(s1.name);

    cout<<"Enter total fees paid: ";
    cin>>s1.FeesPaid;

    cout<<"Enter Stream of learning, such as IT, Finance, Marketing: ";
    gets(s1.stream);

    cout<<"Enter Admission Status-- Either Confirmed or Provisional: ";
    gets(s1.AdmissionStatus);

    cout<<endl<<"The information of the student are: "<<endl;

    cout<<"Name of the Student: "<<s1.name<<endl;
    cout<<"Total Fees Paid Till Now: "<<s1.FeesPaid<<endl;
    cout<<"Stream of Studying: "<<s1.stream<<endl;
    cout<<"Status of admission: "<<s1.AdmissionStatus<<endl;

    return 0;
}
```

Ans. Output of the preceding program is as follows:

```text
Enter student name: Dheeraj
Enter total fees paid: 25000
Enter Stream of learning, such as IT, Finance, Marketing: Human Resource
Enter Admission Status-- Either Confirmed or Provisional: Confirmed

The information of the student are:
Name of the Student: Dheeraj
Total Fees Paid Till Now: 25000
Stream of Studying: Human Resource
Status of admission: Confirmed
```

### Q3. What will be the output of the following program?

```cpp
#include <iostream.h>
#include <stdio.h>

union product
{
        char product_number[15];
        char product_name[30];
        int product_quantity;
        float product_price;
};

void displayNum(product p)
{
        cout<<"Product number :"<<p.product_number<<endl;
}

void displayName(product p)
{
        cout<<"Product name :"<<p.product_name<<endl;
}

void displayQuant(product p)
{
        cout<<"Product quantity :"<<p.product_quantity<<endl;
}

void displayPrc(product p)
{
        cout<<"Product price :"<<p.product_price<<endl;
}

int main()
{
        product p;

        cout<<"Enter product number: ";
        gets(p.product_number);
        displayNum(p);

        cout<<"Enter product name: ";
        gets(p.product_name);
        displayName(p);
        cout<<"Enter product quantity: ";
        cin>>p.product_quantity;
        displayQuant(p);
        int quant = p.product_quantity;

        cout<<"Enter product price of one quantity: ";
        cin>>p.product_price;
        displayPrc(p);

        cout<<"---------------------------------------"<<endl;
        cout<<"Total price = "<<(quant*(p.product_price));

        return 0;
}
```

Ans. The output of the preceding program is as follows:

```text
Enter product number: ABC123
Product number :ABC123
Enter product name: Basket
Product name :Basket
Enter product quantity: 25
Product quantity :25
Enter product price of one quantity: 50
Product price :50
------------------------------------------
Total price = 1250
```

### Q4. What will be the output of the following program?

```cpp
#include <iostream.h>
#include <stdio.h>

struct Student
{
    char name[20];
    int age;
    float marks;
}s1, s2;

int main()
{
    cout<<"Enter Student Name: ";
    gets(s1.name);
    cout<<"Age: ";
    cin>>s1.age;
    cout<<"Marks: ";
    cin>>s1.marks;
    cout<<"\n";
    cout<<"Enter Student Name: ";
    gets(s2.name);
    cout<<"Age: ";
    cin>>s2.age;
    cout<<"Marks: ";
    cin>>s2.marks;
    cout<<"\n";
    cout<<"Displaying the record of student1"<<"\n";
    cout<<"Name: "<<s1.name<<"\n";
    cout<<"Age: "<<s1.age<<"\n";
    cout<<"Marks: "<<s1.marks<<"\n\n";
    cout<<"Displaying the record of student2"<<"\n ";
    cout<<"Name: "<<s2.name<<"\n";
    cout<<"Age: "<<s2.age<<"\n";
    cout<<"Marks: "<<s2.marks<<"\n";

    return 0;
}
```

Ans. The output of the preceding program is as follows:

```text
Enter Student Name: Dheeraj Gupta
Age: 23
Marks: 84

Enter Student Name: Ahmed Umar
Age: 22
Marks: 78

Displaying the record of student1
Name: Dheeraj Gupta
Age: 23
Marks: 84

Displaying the record of student2
Name: Ahmed Umar
Age: 22
Marks: 78
```

### Q5. What will be the output of the following program?

```cpp
#include <iostream.h>

struct name
```
