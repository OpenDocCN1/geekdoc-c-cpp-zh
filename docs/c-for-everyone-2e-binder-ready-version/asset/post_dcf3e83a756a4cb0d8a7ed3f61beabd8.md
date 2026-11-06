
![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_463_0.png)

Write a C++ program that represents a resistor as a class. Provide a single constructor that accepts values for the nominal resistance and tolerance and then determines the actual value randomly. The class should provide public member functions to get the nominal resistance, tolerance, and the actual resistance.

Write a `main` function for the C++ program that demonstrates that the class works properly by displaying actual resistances for ten 330 Ω ±10% resistors.

### Engineering P9.28

In the resistor class from Exercise P9.27, supply a method that returns a description of the “color bands” for the resistance and tolerance. A resistor has four color bands:

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_463_1.png)

- The first band is the first significant digit of the resistance value.
- The second band is the second significant digit of the resistance value.
- The third band is the decimal multiplier.
- The fourth band indicates the tolerance.

| Color | Digit | Multiplier | Tolerance |
| --- | --- | --- | --- |
| Black | 0 | ×10^0 | — |
| Brown | 1 | ×10^1 | ±1% |
| Red | 2 | ×10^2 | ±2% |
| Orange | 3 | ×10^3 | — |
| Yellow | 4 | ×10^4 | — |
| Green | 5 | ×10^5 | ±0.5% |
| Blue | 6 | ×10^6 | ±0.25% |
| Violet | 7 | ×10^7 | ±0.1% |
| Gray | 8 | ×10^8 | ±0.05% |
| White | 9 | ×10^9 | — |
| Gold | — | ×10^-1 | ±5% |
| Silver | — | ×10^-2 | ±10% |
| None | — | — | ±20% |

For example (using the values from the table as a key), a resistor with red, violet, green, and gold bands (left to right) will have 2 as the first digit, 7 as the second digit, a multiplier of $10^5$, and a tolerance of $\pm5\%$, for a resistance of 2,700 kΩ, plus or minus 5%.

### Engineering P9.29

The figure below shows a frequently used electric circuit called a “voltage divider”. The input to the circuit is the voltage $v_i$. The output is the voltage $v_o$. The output of a voltage divider is proportional to the input, and the constant of proportionality is called the “gain” of the circuit. The voltage divider is represented by the equation

$$G = \frac{v_o}{v_i} = \frac{R_2}{R_1 + R_2}$$

where $G$ is the gain and $R_1$ and $R_2$ are the resistances of the two resistors that comprise the voltage divider.

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_464_0.png)

Manufacturing variations cause the actual resistance values to deviate from the nominal values, as described in Exercise P9.27. In turn, variations in the resistance values cause variations in the values of the gain of the voltage divider. We calculate the *nominal value of the gain* using the nominal resistance values and the *actual value of the gain* using actual resistance values.

Write a C++ program that contains two classes, VoltageDivider and Resistor. The Resistor class is described in Exercise P9.27. The VoltageDivider class should have two data members that are objects of the Resistor class. Provide a single constructor that accepts two Resistor objects, nominal values for their resistances, and the resistor tolerance. The class should provide public member functions to get the nominal and actual values of the voltage divider’s gain.

Write a main function for the program that demonstrates that the class works properly by displaying nominal and actual gain for ten voltage dividers each consisting of 5% resistors having nominal values $R_1 = 250\ \Omega$ and $R_2 = 750\ \Omega$.

### ANSWERS TO SELF-CHECK QUESTIONS

- 1. cin is an object, string is a class.
- 2. Through the substr member function and the [] operator.
- 3. As a vector<char>. As a char array.
- 4. None. The member functions will have the same effect, and your code could not have manipulated string objects in any other way.
- 5. 2 1.90
- 6. There is no member function named get_amount_due.
- 7. int get_dollars() const;
- 8. length, substr
- 9. A mutator. Getting a character removes it from the stream, thereby modifying it. Not convinced? Consider what happens if you call the get function twice. You will usually get two different characters. But if you call an accessor twice on an object (without a mutation between the two calls), you are sure to get the same result.
- 10. 2, 1.85, 1, 1.90
- 11. The code tries to access a private data member.
- 12.
  - (1) `int hours; // Between 1 and 12`
    `int minutes; // Between 0 and 59`
    `bool pm; // True for p.m., false for a.m.`
  - (2) `int hours; // Military time, between 0 and 23`
    `int minutes; // Between 0 and 59`
  - (3) `int total_minutes; // Between 0 and 60 * 24 - 1`
- 13. They need not change their programs at all since the public interface has not changed. They need to recompile with the new version of the Time class.
- 14.
  - (1) `string letter_grade; // "A+", "B"`
  - (2) `double number_grade; // 4.3, 3.0`
- 15. (1) The `CashRegister::` is missing. (2) The `const` is missing.
- 16.
  ```cpp
  void CashRegister::add_items(int quantity, double price)
  {
      item_count = item_count + quantity;
      total_price = total_price + quantity * price;
  }
  ```
- 17.
  ```cpp
  int CashRegister::get_dollars() const
  {
      int dollars = total_price; // Truncates cents
      return dollars;
  }
  ```
- 18. Three parameters: two explicit parameters of type int, and one implicit parameter of type string.
- 19. One parameter: the implicit parameter of type string. The function has no explicit parameters.
- 20. `BankAccount::BankAccount() { balance = 0; }`
- 21.
  ```cpp
  BankAccount::BankAccount(double initial_balance)
  {
      balance = initial_balance;
  }
  ```
- 22.
  ```cpp
  Item::Item()
  {
      price = 0;
  }
  ```
  Note that the description data member need not be initialized.
- 23.
  ```cpp
  CashRegister::CashRegister()
  {
      clear();
  }
  ```
- 24. (a) Default constructor. (b) `Item(string)` or `Item(const char[])` (c) `Item(double)` (d) `Item(string, double)` (e) Does not define an object.
- 25.
  ```
  Car my_car

  Car(mpg)
  add_gas(amount)
  drive(distance)
  get_gas_left
  ```

  | gas_left | miles_per_gallon |
  | --- | --- |
  | 0 | 25 |

  front

  back
- 26.
  | gas_left | miles_per_gallon |
  | --- | --- |
  | 0 |  |
  | 20 | 25 |
  | 16 |  |
  | 8 |  |
  | 13 |  |
- 27.
  | gas_left | miles_per_gallon | total_miles |
  | --- | --- | --- |
  | 0 | 25 | 0 |
- 28.
  | gas_left | miles_per_gallon | total_miles |
  | --- | --- | --- |
  | 0 |  | 0 |
  | 20 | 25 |  |
  | 16 |  | 100 |
  | 8 |  | 200 |
  | 13 |  |  |
- 29. Look for nouns in the problem description.
- 30. Yes (ChessBoard) and no (MovePiece).
- 31.
  ![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_466_0.png)
- 32. Typically, a library system wants to track which books a patron has checked out, so it makes more sense to have Patron aggregate Book. However, there is not always one true answer in design. If you feel strongly that it is important to identify the patron

## CHAPTER 10

## INHERITANCE

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_468_0.png)

### CHAPTER GOALS

- To understand the concepts of inheritance and polymorphism
- To learn how to inherit and override member functions
- To be able to implement constructors for derived classes
- To be able to design and use virtual functions

### CHAPTER CONTENTS

- **10.1 INHERITANCE HIERARCHIES** 442
- **10.2 IMPLEMENTING DERIVED CLASSES** 446
  - *Syntax 10.1:* Derived-Class Definition 448
  - *Common Error 10.1:* Private Inheritance 449
  - *Common Error 10.2:* Replicating Base-Class Members 450
  - *Programming Tip 10.1:* Use a Single Class for Variation in Values, Inheritance for Variation in Behavior 450
  - *Special Topic 10.1:* Calling the Base-Class Constructor 451
  - *Syntax 10.2:* Constructor with Base-Class Initializer 451
- **10.3 OVERRIDING MEMBER FUNCTIONS** 451
  - *Common Error 10.3:* Forgetting the Base-Class Name 455
- **10.4 VIRTUAL FUNCTIONS AND POLYMORPHISM** 455
  - *Programming Tip 10.2:* Don’t Use Type Tags 462
  - *Common Error 10.4:* Slicing an Object 462
  - *Special Topic 10.2:* Virtual Self-Calls 463
  - *How To 10.1:* Developing an Inheritance Hierarchy 464
  - *Worked Example 10.1:* Implementing an Employee Hierarchy for Payroll Processing 468
  - *Random Fact 10.1:* The Limits of Parallel Computation 469
