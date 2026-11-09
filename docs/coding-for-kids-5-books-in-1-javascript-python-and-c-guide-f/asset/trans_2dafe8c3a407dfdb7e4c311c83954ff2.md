
## 说明

通过创建结构体，我们创建了一种新的数据类型。

正如我们声明任何变量时通常所做的那样，我们从它将保存的数据类型开始。

在花括号中，我们传入参数，作为所声明结构体变量的值。

参数的顺序很重要。

如果初始化值的数量多于结构体成员，就会报错。

如果值较少，则未出现在列表中的最后几个成员会被初始化为零。

## 访问结构体成员值

要访问结构体成员变量的值，请使用如下所示的点运算符

### 示例代码

```cpp
#include<iostream>
using namespace std;

struct PersonInfo{

    int age;
    int Weight;
    int Height;
};

int main(){

    // initializing the structure
    PersonInfo kevin = {10,50,1};
    PersonInfo jessica = {15,29,1};

    cout << kevin.age << endl;
    cout << jessica.age << endl;

    return 0;
}
```

```text
10
15

Process returned 0 (0x0)    execution time : 0.137 s
Press any key to continue.
```

在上面的输出中，**kevin.age** 和 **jessica.age** 的输出分别是 10 和 15。Age 是结构体的第一个成员。10 和 15 是结构体初始化中的第一个数字，因此它们分别表示凯文和杰西卡的年龄。

## 练习

创建一个名为 Date 的结构体，其中包含成员变量 year、month 和 day。用你当前的日期初始化它，并将所有值打印到屏幕上。

## 最终项目

在最终项目中，我们旨在运用本书中学到的许多技能。

### 任务

设计一个学生管理系统。添加新学生时，输入的信息包括姓名和注册号。用户可以根据注册号搜索特定学生。用户可以查看完整的学生列表，根据注册号删除特定学生，并退出程序。

下面的代码执行该任务；所有任务都会在程序之后清晰解释。

### 代码

```cpp
#include<iostream>
using namespace std;
#include <string>

// search record function to search the record of the student if it exists and then print record
void searchRecord(string name[], string regnum[], string reg, int in) {

    // is found variable to check whether a record exists or not in the array; if it exists set it true
    bool isfound = false;

    // loop till array to check whether a record exists or not
    for(int index = 0; index < in; index = index + 1) {

        // check the every record in array if match then
        if (regnum[index] == reg) {

            // record is found
            isfound = true;

            // printing the record
            cout << "Student Registration Number : " << regnum[index] << "\t" << "Student Name : " << name[index] << endl;
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

int main()
{
    // loop control variable; set it true when the user exits from the programme; set cont false
    bool cont = true;

    // registration number array to store the user registration number
    string registrationNum[100];

    // student name array to store the student name
    string name[100];

    // declaring variable to store the user entered option
    int selectedNumber;

    // index to count the total number of added students
    int index = 0;

    // loop till user exit the programme
    while(cont) {

        // printing menu
        cout << "[1] Create New Record \n"
        <<"[2] Search A Record \n[3] View All Record \n[4] Delete a Record \n[5] Exit  \n"<<endl;

        // prompt user to enter the number
        cout << "Select Number : ";

        // store the user entered number in selectedNumber
        cin >> selectedNumber;

        // if the selectedNumber is 1 then add record into array
        if ( selectedNumber == 1) {

            // declare nam and regNum variables to store the user entered nam and regNum
            string nam;
            string regNum;

            // prompt user to enter name
            cout << "Enter your name : ";

            // store the user entered name into nam variable
            cin >> nam;

            // prompt user to enter the registration number
            cout << "Enter your Registration Number : ";
            cin >> regNum;

            // storing the user entered name and regNum into their respective arrays
            registrationNum[index] = regNum;
            name[index] = nam;

            // incrementing index
            index = index + 1;
            cout << endl;
        }

        // check if user entered 2 then
        else if ( selectedNumber == 2)
        {
            // check if there is at least one record in the array then
            if (index > 0) {

                // prompt user to enter registration number
                string renum;
                cout << "Enter Your Registration Number :";

                // storing the user entered registration number into renum variable
                cin >> renum;

                // calling the function which finds a record and prints it
                searchRecord(name,registrationNum,renum,index);
            }

            // if there is no record in the array then
            else {
                // simply print there is no record in the system
                cout << "There is no Record In the System" << endl;
                cout << endl;
            }
        }

        // check if the user entered number 3 then
        else if (selectedNumber == 3) {

            // Printing all the records of students
            for (int i = 0; i < index; i++) {

                // if there is null in the array which means the record is deleted
                if (name[i] == "null")
                {
                    // just ignore that index
                    continue;
                }
                else {
                    // printing all the records of students
                    cout << " Student Registration Number : " << registrationNum[i] <<
                    "\t\t" << " Student Name : " << name[i] << endl;
                }
            }

            // adding space
            cout << endl;
        }

        // check if the user entered the number 4 then
        else if (selectedNumber == 4) {

            // check if there is any record in the array then
            if (index > 0) {

                // declare the variable renum to store the user registration number
                string renum;

                // prompt user to enter registration number
                cout << "Enter Your Registration Number :";
                cin >> renum;

                // is found variable which checks if the record is found or not in array
                bool isfound = false;

                // loop till the end of number of records
                for(int ind = 0; ind < index; ind = ind + 1){

                    // check if the user entered registration number is equal to registration number in array
                    if (registrationNum[ind] == renum) {

                        // set the value of found to true
                        isfound = true;

                        // adding the null to arrays where value is found
                        name[ind] = "null";
                        registrationNum[ind] = "null";

                        // just print that record deleted successfully
                        cout << " Record deleted successfully : " << endl;
                        cout << endl;
                    }
                }

                // if the user entered registration number is not found then
                if (isfound == false) {
                    // print record is not found
                    cout << " Record is not found : " << endl;
                    cout << endl;
                }
            }

            // if there is no record in the array then
            else {
                // print record does not exist
                cout << "There is no record in the system: " << endl;
                cout << endl;
            }
        }

        // check if the user entered the number 5 then
        else if (selectedNumber == 5) {
            // print take care
            cout << " Take Care " << endl;

            // set cont to false so that programme terminate
            cont = false;
        }
        else {
            // if the user did not enter any number from 1-5 then print please enter valid number
            cout << "Invalid entry : " << endl;
            cout << endl;
        }
    }

    return 0;
}
```

### 输出

```text
[1] Create New Record
[2] Search A Record
[3] View All Record
[4] Delete a Record
[5] Exit

Select Number : 1
Enter your name : john
Enter your Registration Number : 44

[1] Create New Record
[2] Search A Record
[3] View All Record
[4] Delete a Record
[5] Exit

Select Number : 1
Enter your name : jimmy
Enter your Registration Number : 66

[1] Create New Record
[2] Search A Record
[3] View All Record
[4] Delete a Record
[5] Exit

Select Number : 1
Enter your name : hussain
Enter your Registration Number : 12

[1] Create New Record
[2] Search A Record
[3] View All Record
[4] Delete a Record
[5] Exit

Select Number : 2
Enter Your Registration Number :12
Student Registration Number  :  12                  Student Name : hussain
```
