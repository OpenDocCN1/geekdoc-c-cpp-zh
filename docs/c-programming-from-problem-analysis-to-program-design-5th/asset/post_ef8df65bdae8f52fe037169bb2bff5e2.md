
- 29.
  - a. both
  - b. `do ... while`
  - c. while
  - d. while

- 31. In a pretest loop, the loop condition is evaluated before executing the body of the loop. In a posttest loop, the loop condition is evaluated after executing the body of the loop. A posttest loop executes at least once, whereas a pretest loop may not execute at all.

- 33.

  ```cpp
  int num;
  do
  {
      cout << "Enter a number less than 20 or greater than 75: ";
      cin >> num;
  }
  while (20 <= num && num <= 75);
  ```

- 35.

  ```cpp
  int i = 0, value = 0;
  do
  {
      if (i % 2 == 0 && i <= 10)
          value = value + i * i;
      else if (i % 2 == 0 && i > 10)
          value = value + i;
      else
          value = value - i;
      i = i + 1;
  }
  while (i <= 20);

  cout << "value = " << value << endl;
  ```

The Output is: Value = 200

- 37.

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

- 39.
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

- 41. 11 18 25

- 43. -1 0 3 8 15 24

- 45. 12 11 9 7 6 4 2 1

## Chapter 6

- 1. a. false; b. true; c. true; d. true; e. false

- 3. a. 4; b. 10.8; c. 2.5; d. 10.24; e. 15.625; f. 5; g. 2.5; h. 9; i. 28; j. 36

- 5. (iii)

- 7. a, b, c, e, f, and g are valid. In d, the function call in the output (cout) statement requires one more argument.

- 9.
  - a. 4; `int`
  - b. 2; `double`
  - c. 4; `char`
  - d. The function test requires four actual parameters. The order of the parameters is: `int`, `char`, `double`, `int`.
  - e. `cout << test(5, '2', 7.3, 5) << endl;`
  - f. `cout << two(17.5, 18.3) << endl;`
  - g. `cout << static_cast<char>(static_cast<int>(three(4, 3, 'A', 17.6)) + 1) << endl;`

- 11.

  ```cpp
  bool isUppercaseLetter(char ch)
  {
      if (isupper(ch))
          return true;
      else
          return false;
  }
  ```

- 13.
  - a.
    - i. 125
    - ii. 432
  - b. The function computes x³, in which x is the argument of the function.

- 15. 1 4 9 16 25 36 49 64 81 100

- 17.

  ```cpp
  double funcEx17(double x, double y, double z)
  {
      return (x + y) * z;
  }
  ```

## Chapter 7

- 1. a. true; b. false; c. true; d. false; e. true; f. false; g. false; h. false; i. true

- 3.
  - a. A variable declared in the heading of a function definition is called a formal parameter. A variable or expression used in a function call is called an actual parameter.
  - b. A value parameter receives a copy of the actual parameter’s data. A reference parameter receives the address of the actual parameter.
  - c. A variable declared within a function or block is called a local variable. A variable declared outside of every function definition is called a global variable.

- 5.

  ```cpp
  void functionThreeTimes(double x)
  {
      cout << fixed << showpoint << setprecision(2);
      cout << 3 * x << endl;
  }
  ```

- 7.

  ```cpp
  void initialize(int& x, double& y, string& str)
  {
      x = 0;
      y = 0;
      str = "";
  }
  ```

- 9.

  ```text
  5, 10, 15
  20, 10, 15
  25, 30, 15
  45, 30, 60
  ```

- 11.

  ```cpp
  #include <iostream>

  using namespace std;

  void func(int val1, int val2);

  int main()
  {
              int num1, num2;
      __1__   cout << "Please enter two integers." << endl;
      __2__   cin >> num1 >> num2;
      __3__   func(num1, num2);
  ___7___  cout << " The two integers are " << num1
          << ", " << num2 << endl;
  ___8___  return 0;
  }

  void func (int val1, int val2)
  {
          int val3, val4;
     4    val3 = val1 + val2;
  ___5___  val4 = val1 * val2;
  ___6___  cout << "The sum and product are " << val3
              << " and " << val4 << endl;
  }
  ```

- 13.

  ```cpp
  void traceMe(double& x, double y, double& z)
  {
      if (x != 0)
          z = sqrt(y) / x;
      else
      {
          cout << "Enter a nonzero number: ";
          cin >> x;
          cout << endl;
          z = floor(pow(y, x));
      }
  }
  ```

- 15.

  ```text
  10 20
  5 20
  ```

- 17.

  ```text
  11, 3
  16, 2
  19, 3
  24, 2
  ```

- 19. (a), (b), and (d) are correct.

## Chapter 8

- 1. a. true; b. false; c. true; d. false; e. false; f. true; g. true; h. true; i. false; j. false; k. false

- 3. Only a and c are valid.

- 5. The statement:

  `using namespace std;`

  is missing between Lines 1 and 2.

- 7. Either include the statement:

  ```cpp
  using namespace aaa;
  ```

  before the function `main` or refer to the identifiers `x` and `y` in `main` as `aaa::x` and `aaa::y`, respectively.

- 9.

  ```text
  Hello --> Jello
  Bingo --> Ringo
  Sunny --> Bunny
  ```

- 11.

  ```text
  Going to the Amusement Park
  14
  10
  museum
  ABCDEFGHIJK
  11
  aBdEFGHIJK
  ```

## Chapter 9

- 1. a. true; b. true; c. false; d. false; e. true; f. false; g. false; h. false; i. true; j. false; k. false; l. false

- 3.
  - a. This declaration is correct.
  - b. The const declaration should be:

    ```cpp
    const int SIZE = 100;
    double list[SIZE];
    ```

  - c. This declaration should be: `int numList[10];`
  - d. This declaration is correct.
  - e. This declaration should be: `double scores[50];`

- 5. 0 to 49

- 7.

  ```text
  -3 -1 1 3 5
  5 -1 8 3 -1
  ```

- 9. 5 6 9 19 23 37

- 11. If array index is less than 0 or greater than arraySize - 1, we say that the array index is out of bounds. C++ does not check for array indices within bounds.

- 13.
  - a.

    ```cpp
    double heights[10] = {5.2, 6.3, 5.8, 4.9, 5.2, 5.7, 6.7, 7.1, 5.10, 6.0};
    ```

    or

    ```cpp
    double heights[] = {5.2, 6.3, 5.8, 4.9, 5.2, 5.7, 6.7, 7.1, 5.10, 6.0};
    ```

  - b.

    ```cpp
    int weights[7] = {120, 125, 137, 140, 150, 180, 210};
    ```

    or

    ```cpp
    int weights[] = {120, 125, 137, 140, 150, 180, 210};
    ```

  - c.

    ```cpp
    char specialSymbols[] = {'$', '#', '%', '@', '&', '!', '^'};
    ```

  - d.

    ```cpp
    string seasons[4] = {"fall", "winter", "spring", "summer"};
    ```

    or

    ```cpp
    string seasons[] = {"fall", "winter", "spring", "summer"};
    ```

- b. First row of beta: 0 1 2
  Second row of beta: 1 2 3
  Third row of beta: 2 3 4

- c. First row of beta: 0 0 0
  Second row of beta: 0 1 2
  Third row of beta: 0 2 4

- d. First row of beta: 0 2 0
  Second row of beta: 2 0 2
  Third row of beta: 0 2 0

## Chapter 10

- 1. a. false; b. true; c. false; d. false; e. false

- 3.
  - a.

    ```cpp
    int seqOrderedSearch(const int list[], int listLength,
                         int searchItem)
    {
        int loc;
        bool found = false;

        for (loc = 0; loc < listLength; loc++)
            if (list[loc] >= searchItem)
            {
                found = true;
                break;
            }

        if (found)
            if (list[loc] == searchItem)
                return loc;
            else
                return -1;
        else
            return -1;
    }
    ```

  - b.
    - i. 5
    - ii. 7
    - iii. 8
    - iv. 11

- 5.
  - List before the first iteration: 26, 45, 17, 65, 33, 55, 12, 18
  - List after the first iteration: 26, 17, 45, 33, 55, 12, 18, 65
  - List after the second iteration: 17, 26, 33, 45, 12, 18, 55, 65
  - List after the third iteration: 17, 26, 33, 12, 18, 45, 55, 65
  - List after the fourth iteration: 17, 26, 12, 18, 33, 45, 55, 65
  - List after the fifth iteration: 17, 12, 18, 26, 33, 45, 55, 65
  - List after the sixth iteration: 12, 17, 18, 26, 33, 45, 55, 65
  - List after the seventh iteration: 12, 17, 18, 26, 33, 45, 55, 65

- 7. 3
