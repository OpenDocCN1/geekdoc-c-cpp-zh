# View all the records

To view all the record of students, the user presses ‘3’ at the start of the program. There is count variable called *index* which count the number of students. A for loop is used to retrieve each student record and print out each student name and registration number. The loop continues till it reaches the value of *index* which indicates that we are at the end of the array.

```
```cpp
// check if the user entered number 3 then
else if ( selectedNumber == 3 ) {

    // Printing all the records of students
    for (int i = 0; i < index; i++) {

        // if there is null in the array which record is deleted
        if ( name[i] == "null" )
        {
            // just ignore that index
            continue;
        }
        else {
            // printing all the record of student
            cout << "Student Registration Number : " << registrationNum[i] << "\nStudent Name : " << name[i] << endl;
        }
    }

    // adding space
    cout << endl;
}
```
```

# Delete a record

If the user presses ‘4’ at the start of the program, the user can delete a particular student on the basis of registration number. The user first enters the registration number into a variable called *renum*. The program will check if student array is empty then display there is no record in the system if it is empty. If the array is not empty then the program compares the *renum* with registration numbers which are in array *registrationNum*. This is done using a for loop that iterates through the