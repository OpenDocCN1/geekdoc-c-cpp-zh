+   j. An array can be a member of a `struct`. (6, 7)
+   
+   k. A member of a `struct` can be another `struct`. (8)

+   2. Define a `struct` `computerType` to store the following data about a computer: Manufacturer (`string`), model type (`string`), processor type (`string`), ram (`int`) in GB, hard drive size (`int`) in GB, year when the computer was built (`int`), and the price (`double`). (1)

+   3. Assume the definition of Exercise 2. Declare a `computerType` variable and write C++ statements to store the following information: Manufacturer—Computer Corporation, model—Desk Top, processor type—Core I7, RAM—12 GB, hard drive size—500 GB, year when the computer was built—2016, and the price—875.00. (2)

+   4. Consider the declaration of the `struct` `houseType` given in this chapter. Write C++ statements to do the following: (2, 3)
+   
+      a. Declare variables `oldHouse` and `newHouse` of type `houseType`.
+   
+      b. Store the following information into `oldHouse`: Style—Two-story, number of bedrooms—5, number of bathrooms—3, number of cars garage—4, year built—1975, finished square footage—3500, price—675000, and tax = 12500.
+   
+      c. Copy the values of the components of `oldHouse` into the corresponding components of `newHouse`.

+   5. Consider the declaration of the `struct` `houseType` given in this chapter. Suppose `firstHouse` and `secondHouse` are variables of `houseType`. Write C++ statement(s) to compare the style and price of `firstHouse` and `secondHouse`. Output `true` if the corresponding values are the same; `false` otherwise. (2, 3)

+   6. Define a `struct` `fruitType` to store the following data about a fruit: Fruit name (`string`), color (`string`), fat (`int`), sugar (`int`), and carbohydrate (`int`). (1)

+   7. Assume the definition of Exercise 6. Declare a variable of type `fruitType` to store the following data: Fruit name—banana, color—yellow, fat—1, sugar—15, carbohydrate—22. (2)

+   8. Assume the definition of Exercise 6.
+   
+      a. Write a C++ function, `getFruitInput` to read and store data into a variable of `fruitType`.
+   
+      b. Write a C++ function, `printFruitInfo` to output data stored into a variable of `fruitType`. Use appropriate labels to identify each component. (4)

+   9. Which aggregate operations allowed on `struct` variables are not allowed on an array variable? (5)