
You can also calculate the unpaid loan balance after making certain payments. For example, the unpaid balance after making $k$ payments is:

$$L' = R\left[\frac{1-(1+i)^{-(m-k)}}{i}\right]$$

where $R$ is the periodic payment. (Note that if the payments are monthly, then $m = 12$.)

Write a program that prompts the user to input the values of $L$, $r$, $m$, $t$, and $k$. The program then outputs the appropriate values. Your program must contain at least two functions, with appropriate parameters, to calculate the periodic payments and the unpaid balance after certain payments. Make the program menu driven and use a loop so that the user can repeat the program for different values.

- 14. During the tax season, every Friday, the J&J accounting firm provides assistance to people who prepare their own tax returns. Their charges are as follows:

  - a. If a person has low income (<= 25,000) and the consulting time is less than or equal to 30 minutes, there are no charges; otherwise, the service charges are 40% of the regular hourly rate for the time over 30 minutes.

  - b. For others, if the consulting time is less than or equal to 20 minutes, there are no service charges; otherwise, service charges are 70% of the regular hourly rate for the time over 20 minutes.

  (For example, suppose that a person has low income and spent 1 hour and 15 minutes, and the hourly rate is $70.00. Then the billing amount is $70.00 × 0.40 × (45 / 60) = $21.00.)

  Write a program that prompts the user to enter the hourly rate, the total consulting time, and whether the person has low income. The program should output the billing amount. Your program must contain a function that takes as input the hourly rate, the total consulting time, and a value indicating whether the person has low income. The function should return the billing amount. Your program may prompt the user to enter the consulting time in minutes.

- 15. During winter when it is very cold, typically, everyone would like to know the windchill factor, especially, before going out. Meteorologists use the following formula to compute the windchill factor, $W$:

  $$W = 35.74 + 0.6215 \times T - 35.75 \times V^{0.16} + 0.4275 \times T \times V^{0.16},$$

  where $V$ is the wind speed in miles per hour and $T$ is the temperature in degrees Fahrenheit. Write a program that prompts the user to input the wind speed in miles per hour, and the temperature in degrees Fahrenheit. The program then outputs the windchill factor. Your program must contain at least two functions: one to get the user input and the other to determine the windchill factor.

- 16. Consider the definition of the function `main`:

  ```c
  int main()
  {
      int x, y;
      char z;
      double rate, hours;
      double amount;
      .
      .
      .
  }
  ```

  The variables `x`, `y`, `z`, `rate`, and `hours` referred to in items a through f below are the variables of the function `main`. Each of the functions described must have the appropriate parameters to access these variables. Write the following definitions:

  - a. Write the definition of the function `initialize` that initializes `x` and `y` to 0 and `z` to the blank character.

  - b. Write the definition of the function `getHoursRate` that prompts the user to input the hours worked and rate per hour to initialize the variables `hours` and `rate` of the function `main`.

  - c. Write the definition of the value-returning function `payCheck` that calculates and returns the amount to be paid to an employee based on the hours worked and rate per hour. The hours worked and rate per hour are stored in the variables `hours` and `rate`, respectively, of the function `main`. The formula for calculating the amount to be paid is as follows: For the first 40 hours, the rate is the given rate; for hours over 40, the rate is 1.5 times the given rate.

  - d. Write the definition of the function `printCheck` that prints the hours worked, rate per hour, and the salary.

  - e. Write the definition of the function `funcOne` that prompts the user to input a number. The function then changes the value of `x` by assigning the value of the expression two times the (old) value of `x` plus the value of `y` minus the value entered by the user.

  - f. Write the definition of the function `nextChar` that sets the value of `z` to the next character stored in `z`.

  - g. Write the definition of the function `main` that tests each of these functions.

- 17. Consider the following C++ code:

  ```cpp
  #include <iostream>
  #include <cmath>
  #include <iomanip>

  using namespace std;

  void func1();
  void func2(/*formal parameters*/);

  int main()
  {
      int num1, num2;
      double num3;

      int choice;

      cout << fixed << showpoint << setprecision(2);

      do
      {
          func1();
          cin >> choice;
          cout << endl;

          if (choice == 1)
          {
              func2(num1, num2, num3);
              cout << num1 << ", " << num2 << ", " << num3 << endl;
          }
      } while (choice != 99);

      return 0;
  }

  void func1()
  {
      cout << "To run the program, enter 1." << endl;
      cout << "To exit the program, enter 99." << endl;
      cout << "Enter 1 or 99: ";
  }

  void func2(/*formal parameters*/)
  {
      //Write the body of func2.
  }
  ```

  The function func2 has three parameters of type int, int, and double, say a, b, and c, respectively. Write the definition of func2 so that its action is as follows:

  ![](img/b217c421655b51e7494cf3b89bb5432d_508_0.png)

  ```cpp
  while (response == 'y' || response == 'Y')
  {
      cout << "Enter employee's name: ";
      getline(cin, employeeName);
      cout << endl;

      if (isAM == 'y' || isAM == 'Y')
          arrivalAM = true;
      else
          arrivalAM = false;

      cout << "Enter departure hour: ";
      cin >> departureHr;
      cout << endl;
      cout << "Enter departure minute: ";
      cin >> departureMin;
      cout << endl;
      cout << "Enter (y/Y) if departure is before 12:00PM: ";
      cin >> isAM;
      cout << endl;

      if (isAM == 'y' || isAM == 'Y')
          departureAM = true;
      else
          departureAM = false;

      cout << employeeName << endl;
      timeOnJob(arrivalHr, arrivalMin, arrivalAM,
          departureHr, departureMin, departureAM);

      cout << "Enter arrival hour: ";
      cin >> arrivalHr;
      cout << endl;
      cout << "Enter arrival minute: ";
      cin >> arrivalMin;
      cout << endl;
      cout << "Enter (y/Y) if arrival is before 12:00PM: ";
      cin >> isAM;
      cout << endl;

      int arrivalMin;
      bool arrivalAM;
      cout << "Run program again (y/Y): ";
      cin >> response;
      cout << endl;
      cin.get(discard);
  }
  }

  void timeOnJob(int arrHr, int arvMin, bool arvIsAM,
                 int depHr, int depMin, bool depIsAM)
  {
      int arvTimeInMin;
      int depTimeInMin;
      int timeOnJobInMin;

      else if (arvIsAM == true && depIsAM == false)
      {
          arvTimeInMin = arrHr * 60 + arvMin;
          depTimeInMin = depHr * 60 + depMin;

          timeOnJobInMin = (720 - arvTimeInMin) + depTimeInMin;
          cout << "Time spent on job: "
               << timeOnJobInMin / 60 << " hour(s) and "
               << timeOnJobInMin % 60 << " minutes." << endl;
      }
      else
          if (arvTimeInMin <= depTimeInMin)
          {
              timeOnJobInMin = depTimeInMin - arvTimeInMin;
              cout << "Time spent on job: "
                   << timeOnJobInMin / 60 << " hour(s) and "
                   << timeOnJobInMin % 60 << " minutes." << endl;
          }
          else
              cout << "Invalid input." << endl;
      if ((arvIsAM == true && depIsAM == true)
          || (arvIsAM == false && depIsAM == false))
      {
          cout << "Invalid input." << endl;
      }

      void timeOnJob(int arrHr, int arvMin, bool arvIsAM,
                     int depHr, int depMin, bool depIsAM);
  }
  ```

- 19. The function `printGrade` in Example 6-13 is written as a void function to compute and output the course grade. The course score is passed as a parameter to the function `printGrade`. Rewrite the function `printGrade` as a value-returning function so that it computes and returns the course grade. (The course grade must be output in the function `main`.) Also, change the name of the function to `calculateGrade`.

- 20. In this exercise, you are to modify the Classify Numbers programming example in this chapter. As written, the program inputs the data from the standard input device (keyboard) and outputs the results on the standard output device (screen). The program can process only 20 numbers. Rewrite the program to incorporate the following requirements:

  - a. Data to the program is input from a file of an unspecified length; that is, the program does not know in advance how many numbers are in the file.
