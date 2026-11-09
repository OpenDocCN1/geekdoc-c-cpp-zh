```
```cpp
// student name array to store the student registration number
string name[100];

// declaring variable to store the user entered option
int selectedNumber;

// index to count the total number of added student
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
```
```

```
```cpp
if ( selectedNumber == 1) {

    // declare nam and regNum variable to store the user entered nam and regNum
    string nam;
    string regNum;

    // prompt user to enter name
    cout << "Enter your name : ";

    // store the user enter name into nam variable
    cin >> nam;

    //prompt user to enter the registration number
    cout << "Enter your Registration Number : ";
    cin >> regNum;

    // storing the user entered name and regNum into their respective array
    registrationNumber[index] = regNum;
    name[index] = nam;

    // incrementing index
    index = index + 1;
    cout << endl;
}
```
```