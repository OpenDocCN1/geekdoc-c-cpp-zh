
```
[1] Create New Record
[2] Search A Record
[3] View All Record
[4] Delete a Record
[5] Exit

Select Number : 3
Student Registration Number  :  44                 Student Name : john
Student Registration Number  :  66                 Student Name : jimmy
Student Registration Number  :  12                 Student Name : hussain

[1] Create New Record
[2] Search A Record
[3] View All Record
[4] Delete a Record
[5] Exit

Select Number : 4
Enter Your Registration Number :66
Record deleted successfully :

[1] Create New Record
[2] Search A Record
[3] View All Record
[4] Delete a Record
[5] Exit

Select Number : 3
Student Registration Number  :  44                 Student Name : john
Student Registration Number  :  12                 Student Name : hussain

[1] Create New Record
[2] Search A Record
[3] View All Record
[4] Delete a Record
[5] Exit

Select Number : 5
  Take Care

----------------------------------------
Process exited after 40.77 seconds with return value 0
Press any key to continue . . .
```

## 在数组中添加记录

我们已为学生姓名和学生注册号声明了两个数组。这两个数组分别称为 *registrationNum* 和 *name*。

如果用户输入数字“1”，程序将要求用户输入学生姓名和注册号。然后用户输入姓名和注册号。它们会被存储到各自的数组中。有一个名为 *index* 的计数变量，用于统计已创建的学生数量。每添加一名学生，索引就增加 1。添加记录的过程如下方代码部分所示。

```cpp
if ( selectedNumber == 1) {

    // declare nam and regNum variable to store the user entered nam and regNum
    string nam;
    string regNum;

    // prompt user to enter name
    cout << "Enter your name : ";

    // store the user entered name into nam variable
    cin >> nam;

    // prompt user to enter the registration number
    cout << "Enter your Registration Number : ";
    cin >> regNum;

    // storing the user entered name and regNum into their respective array
    registrationNum[index] = regNum;
    name[index] = nam;

    // incrementing index
    index = index + 1;
    cout << endl;
}
```

## 从数组中搜索记录

用户可以在程序开始时按“2”，使用其登记注册号搜索特定学生。
程序首先检查学生数组是否为空。如果数组不为空，用户随后输入注册号。程序将用户输入的注册号与数组中已有的注册号进行比较。它使用函数 *searchRecord()* 来完成此操作。

```cpp
}
// check if user entered 2 then
else if ( selectedNumber == 2)
{
    // check if there is at least one record in the array then
    if ( index >= 0) {
        // prompt user to enter registration number
        string renum;
        cout << "Enter Your Registration Number :";

        // storing the user entered registration number into renum variable
        cin >> renum;

        // calling the function which find a record and print it
        searchRecord(name,registrationNum,renum,index);
    }
}
// if there is no record in the array then
```

函数 **searchRecord()** 接收姓名数组（**name[]**）和注册号数组（**regnum[]**）作为参数。它还接收两个变量：注册号 **reg** 和索引 **in**。
**reg** 是我们用于搜索学生记录的注册号，而 **in** 是记录数量。
该函数使用 for 循环在数组 **regnum[]** 中搜索注册号 **reg**。
如果找到 **reg**，该函数会打印学生注册号和姓名。
如果未找到 **reg**，该函数会打印“未找到记录”。

```cpp
// search record function to search the record of the student if it exists and then print record
void searchRecord(string name[], string regnum[], int reg, int in) {
    // isfound variable to check whether a record exists or not in the array; if exists set it true
    bool isfound = false;

    // loop through the array to check whether a record exists or not
    for(int index = 0; index < in; index = index + 1) {
        // check every record in array if match then
        if (regnum[index] == reg) {
            // record is found
            isfound = true;

            // printing the record
            cout << "Student Registration Number : " << regnum[index] << "\t\t" << "Student Name : " << name[index] << endl;
            cout << endl;

            // terminating from loop
            break;
        }
    }

    // if a particular record does not exist then
    if (isfound == false) {
        // display that record does not exist
        cout << "Record is not found : " << endl;
        cout << endl;
    }
}
```

## 查看所有记录

要查看所有学生记录，用户在程序开始时按“3”。有一个名为 *index* 的计数变量，用于统计学生数量。使用 for 循环检索每条学生记录，并打印每个学生姓名和注册号。循环持续到达到 *index* 的值，这表示已到达数组末尾。

```cpp
// check if the user entered number 3 then
else if ( selectedNumber == 3 ) {

    // Printing all the records of students
    for (int i = 0; i < index; i++) {

        // if there is null in the array where a record is deleted
        if ( name[i] == "null" )
        {
            // just ignore that index
            continue;
        }
        else {
            // printing all the records of students
            cout << "Student Registration Number : " << registrationNum[i] << "\nStudent Name : " << name[i] << endl;
        }
    }

    // adding space
    cout << endl;
}
```

## 删除记录

如果用户在程序开始时按“4”，可以基于注册号删除特定学生。用户首先将注册号输入名为 *renum* 的变量。程序将检查学生数组是否为空；如果为空，则显示系统中没有记录。如果数组不为空，程序会将 *renum* 与数组 *registrationNum* 中的注册号进行比较。这是通过遍历数组的 for 循环完成的。如果找到该学生，则通过将相关 name 和 registrationNum 设为 null 来从数组中删除该记录。如果未找到该学生记录，程序会打印“未找到记录”。

```cpp
// check if the user entered the number 4 then
else if ( selectedNumber == 4 ) {

    // check if there is any record in the array then
    if ( index >= 0 ) {

        // declare the variable renum to store the user registration number
        string renum;

        // prompt user to enter registration number
        cout << "Enter Your Registration Number :";
        cin >> renum;

        // isfound variable which checks if the record is found or not in the array
        bool isfound = false;

        // loop till the end of number of records
        for(int ind = 0; ind < index; ind = ind + 1 ) {

            // check if the user entered registration number is equal to registration num in array
            if ( registrationNum[ind] == renum ) {

                // set the value of found to true
                isfound = true;

                // assigning null to the arrays where the value is found
                name[ind] = "null";
                registrationNum[ind] = "null";

                // first print that record deleted successfully
                cout << " Record deleted successfully : " << endl;
                cout << endl;
            }
        }

        // if the user entered registration number is not found then
        else {

            // if there is no record in the array then
            else {

                // print record does not exist
                cout << " There is no record in the system: " << endl;
                cout << endl;
            }
        }
    }
}
```

## 退出

如果用户输入数字“5”，则直接跳出循环。
