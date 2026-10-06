# 6. Days of Each Month

Design a program that displays the number of days in each month. The program's output should be similar to this:

```
January has 31 days.
February has 28 days.
March has 31 days.
April has 30 days.
May has 31 days.
June has 30 days.
July has 31 days.
August has 31 days.
September has 30 days.
October has 31 days.
November has 30 days.
December has 31 days.
```

The program should have two parallel arrays: a 12-element String array that is initialized with the names of the months, and a 12-element Integer array that is initialized with the number of days in each month. To produce the output, use a loop to step through the arrays getting a name of a month and the number of days in each.

# 7. Phone Number Lookup

Design a program that has two parallel arrays: a String array named people that is initialized with the names of your friends, and a String named phoneNumbers that is initialized with your friend's phone numbers. The program should allow the user to enter a person's name (or part of a person name). It should search for that in the people array. If the person is found, it should get that person's phone number from the phoneNumbers array and display it. If the person is not found in the people array, the program should display a message indicating so.

# 8. Payroll

Design a program that uses the following parallel arrays:

+   - empId: An array of seven Integers to hold employee identification numbers.
The array should be initialized with the following numbers:
  65588 45201 78951 84512 13028 75804
- hours: An array of seven Integers to hold the number of hours worked by each employee.
- payRate: An array of seven Reals to hold each employee's hourly pay rate.
- wages: An array of seven Reals to hold each employee's gross wages.

The program should read the data in each array through the subscripts. For example, the number in element 0 of the hours worked by the employee whose identification number is stored in element 0 of the empId array. That employee's pay rate should be stored in element 0 of the payRate array.

The program should display each employee name and ask the user to enter that employee's hours and pay rate (hours times rate), which should be stored in the wages array. After the data has been entered for all the employees, the program should display each employee's identification number and gross wages.