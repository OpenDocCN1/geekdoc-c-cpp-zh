
28. To close a file as indicated by the `ifstream` variable `inFile`, you use the statement `inFile.close();`. To close a file as indicated by the `ofstream` variable `outFile`, you use the statement `outFile.close();`.

## EXERCISES

The number in parentheses at the end of an exercise refers to the learning objective listed at the beginning of the chapter.

1. **Mark the following statements as true or false.**
   - a. An output stream is a sequence of characters from a computer to an output device. (1)
   - b. To use `cin` and `cout` in a program, the program must include the header file `iostream`. (1, 2)
   - c. Suppose `pay` is a variable of type `double`. The statement `cin >> pay;` requires the input of a decimal number. (2)
   - d. The statements `cin >> length;` and `length >> cin;` are equivalent. (2)
   - e. When the statement `cin >> num1 >> num2;` executes, then after inputting a number into the variable `num1` the program skips all trailing whitespace characters. (2)
   - f. To use the predefined function `sqrt` in a program, the program must include the header file `math`. (3)
   - g. The statement `cin.get(ch);` inputs the next nonwhitespace character into the variable `ch`. (4)
   - h. When the input stream enters the fail state, the program terminates with an error message. (5)
   - i. To use the manipulators `fixed` and `showpoint`, the program does not require the inclusion of the header file `iomanip`. (6)
   - j. The statement `cin >> right;` sets the input of only the next variable right-justified. (7)
   - k. To input data from a file, the program must include the header file `fstream`. (10)

2. Suppose `x`, `y`, and `z` are `int` variables and `ch` is a `char` variable. Consider the following input: (2)

   ```
   78 86 18 #42 &
   ```

   What value (if any) is assigned to `x`, `y`, `z`, and `ch` after each of the following statements executes? (Use the same input for each statement.)

   - a. `cin >> x >> y >> z >> ch;`
   - b. `cin >> ch >> x >> y >> z;`
   - c.
     ```cpp
     cin >> x;
     cin.get(ch);
     cin >> y >> z;
     ```
   - d.
     ```cpp
     cin >> x >> ch >> y >> z;
     cin.get(ch);
     ```
   - e.
     ```cpp
     cin >> x >> y >> z;
     ```

3. Suppose `int1` and `int2` are int variables and `dec1` and `dec2` are double variables. Assume the following input data: (2)

   ```
   56.50 67 48 62.72
   ```

   What value (if any) is assigned to `int1`, `int2`, `dec1`, and `dec2` after each of the following statements executes? (Use the same input for each statement.)

   - a. `cin >> dec1 >> int1 >> int2 >> dec2;`
   - b. `cin >> int1 >> dec1 >> dec2 >> int1;`
   - c. `cin >> dec1 >> dec2 >> int1 >> int2;`
   - d. `cin >> int1 >> dec1 >> int2 >> dec2;`
   - e. `cin >> int1 >> int2 >> dec1 >> dec2;`

4. Suppose `x` and `y` are int variables and `symbol` is a char variable. Assume the following input data:

   ```
   38 26 * 67 33
   24 $ 55 # 34
   # & 63 85
   ```

   What value (if any) is assigned to `x`, `y`, and `symbol` after each of the following statements executes? (Use the same input for each statement.)

   (2, 3, 4)

   - a.
     ```cpp
     cin >> x >> y;
     cin.ignore(100, '\n');
     cin >> symbol;
     ```
   - b.
     ```cpp
     cin >> x;
     cin.ignore(100, '*');
     cin >> y;
     cin.get(symbol);
     ```
   - c.
     ```cpp
     cin >> y;
     cin.ignore(100, '\n');
     cin >> x >> symbol;
     ```
   - d.
     ```cpp
     cin.get(symbol);
     cin.ignore(100, '*');
     cin >> x;
     cin.ignore(100, '\n');
     cin >> y;
     ```
   - e.
     ```cpp
     cin.ignore(100, '\n');
     cin >> x >> symbol;
     cin.ignore(100, '\n');
     cin.ignore(100, '&');
     cin >> y;
     ```

5. Given the input:

   ```
   Samantha 168.5 46
   ```

   and the variable declaration: (2, 8)

   ```cpp
   double dec = 2.7;
   int num = 45;
   string str = "***";
   ```

   What is the output, if any? Use the same input for each part.

   - a.
     ```cpp
     cin >> str >> dec >> num;
     cout << str << " " << dec << " " << num << endl;
     ```
   - b.
     ```cpp
     cin >> str >> num >> dec;
     cout << str << " " << dec << " " << num << endl;
     ```
   - c.
     ```cpp
     cin >> dec >> str >> num;
     cout << str << " " << dec << " " << num << endl;
     ```

6. Suppose that int1 and int2 are int variables, dec is a double variable, and ch is a char variable. Suppose the input statement is:

   ```cpp
   cin >> int1 >> ch >> int2 >> dec;
   ```

   What values, if any, are stored in int1, int2, dec, and ch if the input is: (2)

   - a. 13 24 16.2
   - b. 45 $36 9.2
   - c. 16 #.75 72

7. What does function `pow` do? Which header file must be included to use the function `pow`? (3)

8. What does function `sqrt` do? Which header file must be included to use the function `sqrt`? (3)

9. What is the purpose of the manipulator `setprecision`? Which header file must be included to use the function `setprecision`? (7)

10. Which header file must be included to use the manipulators `fixed` and `showpoint`? (7)

11. What is the purpose of the manipulator `setw`? Which header file must be included to use the function `setw`? (7)

12. What is the output of the following program? (2, 3, 6, 8)

    ```cpp
    #include <iostream>
    #include <cmath>
    #include <string>
    #include <iomanip>

    using namespace std;

    int main()
    {
        double x, y;
        string str;

        x = 9.0;
        y = 3.2;

        cout << fixed << showpoint << setprecision(2);

        cout << x << "^" << y << " = " << pow(x, y) << endl;
        cout << "5.0^2.5 = " << pow(5.0, 2.5) << endl;
        cout << "sqrt(48.35) = " << sqrt(48.35) << endl;

        cout << "static_cast<int>(sqrt(pow(y, 4))) = "
             << static_cast<int>(sqrt(pow(y, 4))) << endl;

        str = "Predefined functions simplify programming code!";

        cout << "Length of str = " << str.length() << endl;

        return 0;
    }
    ```

13. To use the functions `peek` and `putback` in a program, which header file(s) must be included in the program? (4)

14. Suppose that `num` is an `int` variable and `discard` is a `char` variable. Assume the following input data:

    ```
    #34
    ```

    What value (if any) is assigned to `num` and `discard` after each of the following statements executes? (Use the same input for each statement.) (2, 4)

    - a.
      ```cpp
      cin.get(discard);
      cin >> num;
      ```
    - b.
      ```cpp
      discard = cin.peek();
      cin >> num;
      ```
    - c.
      ```cpp
      cin.get(discard);
      cin.putback(discard);
      cin >> discard;
      cin >> num;
      ```

15. Suppose that `name` is a variable of type `string`. What is the effect of the following statement? (8)

    ```cpp
    getline(cin, name);
    ```

16. Write a C++ statement that uses the manipulator `setfill` to output a line containing 35 stars, as in the following line: (7)

    ```
    ***********************************
    ```

17. Suppose that `height` is a `double` variable and `name` is a `string` variable. What are the values of `height` and `name` after the following input statements execute: (8)

    ```cpp
    cin >> height;
    getline(cin, name);
    ```

    if the input is:

    - a. `5.4 Christy Miller`
    - b.
      ```
      5.4
      Christy Miller
      ```

18. Suppose that `height` is a `double` variable, `ch` is a `char` variable, and `name` is a `string` variable. What are the values of `height` and `name` after the following input statements execute: (8)

    ```cpp
    cin >> height;
    cin.get(ch);
    getline(cin, name);
    ```

    if the input is:

    - a. `5.4 Christy Miller`
    - b.
      ```
      5.4
      Christy Miller
      ```

19. The following program is supposed to read the length and width of a rectangle from a file named `input.txt` and write the area and perimeter of the numbers to a file named `output.txt`. However, it fails to do so. Rewrite the program so that it accomplishes what it is intended to do. (Also, include statements to close the files.) (10)

    ```cpp
    #include <iostream>

    using namespace std;

    int main()
    {
        double length, width;
        ofstream outfile;

        infile.open("input.txt");

        infile >> length >> width;
        outfile << "Area = " << length * width
                << ", Perimeter = " << 2 * (length + width) << endl;
        return 0;
    }
    ```
