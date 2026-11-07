
## Chapter 3

- **1.** a. true; b. true; c. false; d. false; e. false; f. true; g. false; h. false; i. true; j. false; k. true

- **3.**
  - a. `int1 = 67, int2 = 48, dec1 = 56.5, dec2 = 62.72`
  - b. `int1 = 48, int2 = -1, dec1 = 0.5, dec2 = 67`
  - c. `int1 = 48, int2 = 62, dec1 = 56.5, dec2 = 67`
  - d. `int1 = 56, int2 = 67, dec1 = 0.5, dec2 = 48`
  - e. Input failure: `int1 = 56`; trying to read the `.` (period) into `int2`.

- **5.**
  - a. `Samantha 168.5 46`
  - b. `Samantha 0.5 168`
  - c. `** 2.7 45`

  Input failure: Trying to read `s` into `dec`, which is a `double` variable. The values of `dec`, `num`, and `str` are unchanged.

- **7.** The function `pow` calculates x^y in a program. That is, `pow(x, y) = x^y`. To use this function the program must include the header file `cmath`.

- **9.** The manipulator `scientific` is used to output floating-point numbers in scientific format. To use this function the program must include the header file `iomanip`.

- **11.** The manipulator `setw` is used to output the value of an expression in a specific number of columns. To use this function the program must include the header file `iomanip`.

- **13.** `iostream`

- **15.** The function `getline` reads until it reaches the end of the current line. The newline character is also read but not stored in the `string` variable.

- **17.**
  - a. `name = " Christy Miller", height = 5.4`
  - b. `name = " ", height = 5.4`

- **19.**

    ```cpp
    #include <iostream>
    #include <fstream>

    using namespace std;

    int main()
    {
        int num1, num2;
        ifstream infile;
        ofstream outfile;

        infile.open("input.dat");
        outfile.open("output.dat");

        infile >> num1 >> num2;
        outfile << "Sum = " << num1 + num2 << endl;

        infile.close();
        outfile.close();

        return 0;
    }
    ```

- **21.** `fstream`

- **23.**
  - a. Same as before.
  - b. The file contains the output produced by the program.
  - c. The file contains the output produced by the program. The old contents are erased.
  - d. The program would prepare the file and store the output in the file.

- **25.**
  - a. `outfile.open("sales.dat");`
  - b. `outfile << fixed << showpoint << setprecision(2);`
  - c. `revenue = numOfJuiceBottlesSold * costOfaJuiceBottle;`
  - d. `outfile << numOfJuiceBottlesSold << " " << costOfaJuiceBottle << " " << revenue << endl;`
  - e. `outfile.close();`

## Chapter 4

- **1.** a. false; b. false; c. false; d. false; e. true; f. false; g. false; h. false; i. false; j. false; k. false

- **3.** a. false; b. true; c. true; d. true

- **5.**
  - a. `x == z: 0`
  - b. `y != z - 9: 0`
  - c. `x - y == z + 10: 1`
  - d. `!(z < w): 1`
  - e. `w - y < x - 2 * z: 0`

- **7.**
  - a. `++x`
  - b. `12 / 2 != 4 + 1`
  - c. `*`
  - d. **C++**
  - e. **low**  
    **high**

- **9.**
  - a. `%!!`
  - b. `a b c d`  
    `##`
  - c. `Flying Coding`

- **11.** The value of don is: 0

- **13.** Omit the semicolon after `else`. The correct statement is:

    ```cpp
    if (score >= 60)
        cout << "Pass" << endl;
    else
        cout << "Fail" << endl;
    ```

- **15.** The correct code is:

    ```cpp
    if (numOfItemsBought > 10)
        shippingCharges = 0.0;
    else if (5 <= numOfItemsBought && numOfItemsBought <= 10)
        shippingCharges = 3.00 * numOfItemsBought;
    else if (0 < numOfItemsBought && numOfItemsBought < 5)
        shippingCharges = 7.00 * numOfItemsBought;
    ```

- **17.** `20 10`

- **19.**

    ```cpp
    if (sale > 20000)
        bonus = 0.10;
    else if (sale > 10000 && sale <= 20000)
        bonus = 0.05;
    else
        bonus = 0.0;
    ```

- **21.**
  - a. The output is: **Discount = 10%**. The semicolon at the end of the `if` statement terminates the `if` statement. So the `cout` statement is not part of the `if` statement. The `cout` statement will execute regardless of whether the expression in the `if` statement evaluates to `true` or `false`.
  - b. The output is: **Discount = 10%**. The semicolon at the end of the `if` statement terminates the `if` statement. So the `cout` statement is not part of the `if` statement. The `cout` statement will execute regardless of whether the expression in the `if` statement evaluates to `true` or `false`.

- **23.**
  - a. `(x == y) ? z = x + y : z = (x + y) / 2;`
  - b.

    ```cpp
    (hours >= 40.0) ? wages = 40 * 7.50 + 1.5 * 7.5 *
                             (hours - 40)
                      : wages = hours * 7.50;
    ```

  - c. `(loanAmount >= 200000) ? closingCosts = 10000 : closingCosts = 8000;`

- **25.** a. 40.00 b. 40.00 c. 55.00

- **27.** a. 8 b. 64 c. 1 d. 12

- **29.** a. 7 b. 12167 c. 8000 d. 3

- **31.**

    ```cpp
    #include <iostream>

    using namespace std;
    const int SECRET = 5;

    int main()
    {
        int x, y, w, z;

        z = 9;

        if (z > 10)
        {
            x = 12;
            y = 5;
            w = x + y + SECRET;
        }
        else
        {
            x = 12;
            y = 4;
            w = x + y + SECRET;
        }

        cout << "w = " << w << endl;

        return 0;
    }
    ```

- **33.**

    ```cpp
    switch (classStanding)
    {
        case 'f':
            dues = 150.00;
            break;
        case 's':
            if (gpa >= 3.75)
                dues = 75.00;
            else
                dues = 120.00;
            break;
        case 'j':
            if (gpa >= 3.75)
                dues = 50.00;
            else
                dues = 100.00;
            break;
        case 'n':
            if (gpa >= 3.75)
                dues = 25.00;
            else
                dues = 75.00;
            break;
        default:
            cout << "Invalid class standing code." << endl;
    }
    ```

## Chapter 5

- **1.** a. true; b. false; c. true; d. false; e. true; f. true; g. true; h. false; i. false; j. true

- **3.** 40

- **5.** `if (ch > 'Z' || ch < 'A')`

- **7.** Sum = 22

- **9.** temp = 0

- **11.**
  - a. 20  *
  - b. *
  - c. 41 70 111  *
  - d. 27 44 71  *

- **13.** Replace the while loop statement with the following:

    ```cpp
    while (response == 'Y' || response == 'y')
    ```

    Replace the cout statement

    ```cpp
    cout << num1 << " + " << num2 << " = " << (num1 - num2)
         << endl;
    ```

    with the following:

    ```cpp
    cout << num1 << " + " << num2 << " = " << (num1 + num2)
         << endl;
    ```

- **15.** `2  3  4  5  6`

- **17.** `0  3  8  15  24`

- **19.**
  - Loop control variable: `j`
  - The initialization statement: `j = 1;`
  - Loop condition: `j <= 10;`
  - Update statement: `j++`
  - The statement that updates the value of `s`: `s = s + j * (j - 1);`

- **21.** `num = 485, y = 15`

- **23.**
  - a. `*`
  - b. `infinite loop`
  - c. `infinite loop`
  - d. `****`
  - e. `******`
  - f. `***`

- **25.** The relationship between x and y is: `3^y = x`

  Output: `x = 19683, y = 10`

- **27.**

    ```
    0 - 24
    25 - 49
    50 - 74
    75 - 99
    100 - 124
    125 - 149
    150 - 174
    175 - 200
    ```

- **29.**
  - a. both
  - b. do ... while
  - c. while
  - d. while

- **31.** In a pretest loop, the loop condition is evaluated before executing the body of the loop. In a posttest loop, the loop condition is evaluated after executing the body of the loop. A posttest loop executes at least once, while a pretest loop may not execute at all.

- **33.**

    ```cpp
    int num;
    do
    {
        cout << "Enter a number less than 20 or greater than 75: ";
        cin >> num;
    }
    while (20 <= num && num <= 75);
    ```

- **35.**

    ```cpp
    int i = 0, value = 0;
    do
    {
        if (i % 2 == 0 && i <= 10)
            value = value + i;
        else if (i % 2 == 0 && i > 10)
            value = value + i;
        else
            value = value - i;
        i = i + 1;
    }
    while (i <= 20);

    cout << "value = " << value << endl;
    ```

  The output is: `value = 200`

- **37.**

    ```cpp
    cin >> number;
    while (number != -1)
    {
        total = total + number;
        cin >> number;
    }
    cout << endl;
    cout << total << endl;
    ```

- **39.**
  - a.

    ```cpp
    number = 1;
    while (number <= 10)
    {
        cout << setw(3) << number;
        number++;
    }
    ```

  - b.

    ```cpp
    number = 1;
    do
    {
        cout << setw(3) << number;
        number++;
    }
    while (number <= 10);
    ```

- **41.**
  - a. 36 94 260
  - b. 4 20
  - c. 30
  - d. 98 250

- **43.** -1 0 3 8 15 24

- **45.** 12 11 9 7 6 4 2 1

## Chapter 6

- **1.** a. false; b. true; c. true; d. true; e. false; f. false; g. true; h. false; i. true; j. true; k. false; l. false; m. false; n. true

- **3.** a. 18 b. 20.50 c. 87.20 d. 16.00 e. 1717.82 f. 2.80 g. 14.00 h. 11.16 i. 27.00 j. 20.00 k. 19.00 m. 2.25 n. 4096.00 o. 0.01 p. 3.03

- **5.** a and b

- **7.** a, b, c, d, and e are valid. In f, the second argument in the function call is missing. In g and h, the function call requires one more argument.

- **9.**
  - a. 2; double
  - b. 3; int
  - c. 3; string
