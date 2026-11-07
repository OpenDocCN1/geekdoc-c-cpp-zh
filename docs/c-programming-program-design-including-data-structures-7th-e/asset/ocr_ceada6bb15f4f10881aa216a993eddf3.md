+   d. A struct member is accessed by using the operator `. (2)`

+   e. The only allowable operations on a struct are assignment and member selection. (2)

+   f. Because a struct has a finite number of components, relational operations are allowed on a struct. (2)

+   g. Some aggregate input/output operations are allowed on a struct variable. (2)

+   h. A struct variable can be passed as a parameter either by value or by reference. (4)

+   i. A function cannot return a value of the type struct. (4)

+   j. An array can be a member of a struct. (6, 7)

+   k. A member of a struct can be another struct. (8)

2. Define a struct, `carType`, to store the following data about a car: Manufacturer (string), model (string), model type (string), color (string), number of doors (int), miles per gallon in city (int), miles per gallon on highway (int), year when the car was built (int), and the price (double). (1)

3. Assume the definition of Exercise 2. Declare a `carType` variable and write C++ statements to store the following information: Manufacturer—GMT, model—Cylone, type—sedan, color—blue, number of doors—4, miles per gallon in city—28, miles per gallon on highway—32, year when the car was built—2006, and the price—25000.00. (2)

4. Define a struct, `fruitType`, to store the following data about a fruit: Fruit name (string), color (string), fat (int), sugar (int), carbohydrate (int). (1)

5. Assume the definition of Exercise 4. Declare a variable of type `fruitType` to store the following data: Fruit name—banana, color—yellow, fat—1, sugar—15, carbohydrate—22. (2)

6. Consider the declaration of the struct `houseType` given in this chapter. Write C++ statements to do the following: (2, 3)

+   a. Declare variables `oldHouse` and `newHouse` of type `houseType`.

+   b. Store the following information into `oldHouse`: Style—Two-story, number of bedrooms—5, number of bathrooms—3, number of cars garage—4, year built—1975, finished square footage—3500, price—675000, and tax—12500.

+   c. Copy the values of the components of `oldHouse` into the corresponding components of `newHouse`.

7. Consider the declaration of the struct `houseType` given in this chapter. Suppose `firstHouse` and `secondHouse` are variables of `houseType`. Write C++ statement(s) to compare the style and price of `firstHouse` and `secondHouse`. Output true if the corresponding values are the same; false otherwise. (2, 3)