
You are given the number of rows and columns. For any row or column number, you can query the color, which will be red, black, or something else. If you find that the center of the black pixels coincides with the center of the red pixels, you have found a red eye, and your output should be "yes". Otherwise, your output is "no".

![](img/d61019b035dd82beb581604273c0ee6b_59_0.png)

## Engineering R1.28

The San Francisco taxi commission set the following rates for 2017:

- First 1/5th of a mile: $3.50
- Each additional 1/5th of a mile or fraction thereof: $0.55
- Each minute of waiting or traffic delay: $0.55

The charge for "waiting or traffic delay" applies instead of the mileage charge for each minute in which the speed is slower than the break-even point. The break-even point is the speed at which 1/5th of a mile is traversed in one minute. Develop an algorithm that yields the fare for traveling a given distance in a given amount of time, assuming that the taxi moves at a constant speed.

![](img/d61019b035dd82beb581604273c0ee6b_59_1.png)

## Engineering R1.29

Suppose you know how long it takes a car to accelerate from 0 to 60 miles per hour.

Develop an algorithm for computing the time required to travel a given distance (for example 5 miles), assuming that the car is initially at rest, accelerates to a given speed (for example 25 miles per hour), and drives at that speed until the distance is covered. Hint: An object that starts at rest and accelerates at a constant rate a for t seconds travels a distance of s = 1/2 a t².

## Engineering R1.30

Taxi meters measure the distance traveled by counting the number of revolutions of an axle.

The meter is initialized by driving a known distance. A disreputable taxi driver tricks his customers into paying more per trip. He does this by slightly deflating his taxi’s tires after the meter has been initialized, so that they have a smaller radius. This way, the tire will have a greater number of revolutions per trip, making each trip appear to be a greater number of miles. Develop an algorithm for computing what the deflated tire radius must be if the taxi driver would like a short x-mile taxi ride to appear to be a longer y-mile taxi ride. Inputs are the proper tire radius R and the distances x and y.

## PRACTICE EXERCISES

- **E1.1** Write a program that prints a greeting of your choice, perhaps in a language other than English.
- **E1.2** Write a program that prints the sum of the first ten positive integers, 1 + 2 + ⋯ + 10.
- **E1.3** Write a program that prints the product of the first ten positive integers, 1 × 2 × ⋯ × 10. (Use * to indicate multiplication in C++.)
- **E1.4** Write a program that prints the balance of an account after the first, second, and third year. The account has an initial balance of $1,000 and earns 5 percent interest per year.
- **E1.5** Write a program that displays your name inside a box on the screen, like this: Dave

  Do your best to approximate lines with characters such as | - +.
- **E1.6** Write a program that prints your name in Morse code, like this:

  .... . .-.. .--.  -.-. . .-. . .-. . . .--. .

  Use a separate output statement for each letter.
- **E1.7** Write a program that prints three items, such as the names of your three best friends or favorite movies, on three separate lines.
- **E1.8** Write a program that prints a poem of your choice. If you don't have a favorite poem, search the Internet for "Emily Dickinson" or "e e cummings".
- **Business E1.9** Write a program that prints a two-column list of your friends' birthdays. In the first column, print the names of your best friends; in the second, print their birthdays.
- **Business E1.10** In the United States there is no federal sales tax, so every state may impose its own sales taxes. Look on the Internet for the sales tax charged in five U.S. states, then write a program that prints the tax rate for five states of your choice.

  ```text
  Sales Tax Rates
  ----------------
  Alaska: 0%
  Hawaii: 4%
  ...
  ```

- **Business E1.11** To speak more than one language is a valuable skill in the labor market today. One of the basic skills is learning to greet people. Write a program that prints a two-column list with the greeting phrases shown in the table. In the first column, print the phrase in English, in the second column, print the phrase in a language of your choice. If you don't speak a language other than English, use an online translator or ask a friend.

  | List of Phrases to Translate |
  | --- |
  | Good morning. |
  | It is a pleasure to meet you. |
  | Please call me tomorrow. |
  | Have a nice day! |

- **Engineering E1.12** Write a program that prints out the following English/metric conversions:

  1 kilogram = 2.21 pounds
  1 pound = 0.454 kilograms
  1 foot = 0.305 meters
  1 meter = 3.28 feet
  1 mile = 1.61 kilometers
  1 kilometer = 0.621 miles

## PROGRAMMING PROJECTS

- **P1.1** Write a program that prints the message, “Hello, my name is Hal!” Then, on a new line, the program should print the message “What would you like me to do?” Then it’s the user’s turn to type in an input. You haven’t yet learned how to do it—just use the following lines of code:

  ```cpp
  string user_input;
  getline(cin, user_input);
  ```

  Finally, the program should ignore the user input and print the message “I am sorry, I cannot do that.”

  This program uses the string data type. To access this feature, you must place the line

  ```cpp
  #include <string>
  ```

  before the main function.

  Here is a typical program run. The user input is printed in color.

  ```
  Hello, my name is Hal!
  What would you like me to do?
  Clean up my room
  I am sorry, I cannot do that.
  ```

  When running the program, remember to press the Enter key after typing the last word of the input line.

- **P1.2** Write a program that prints out a message “Hello, my name is Hal!” Then, on a new line, the program should print the message “What is your name?” As in Exercise P1.1, just use the following lines of code:

  ```cpp
  string user_name;
  getline(cin, user_name);
  ```

  Finally, the program should print the message “Hello, user name. I am glad to meet you!” To print the user name, simply use

  ```cpp
  cout << user_name;
  ```

  As in Exercise P1.1, you must place the line

  ```cpp
  #include <string>
  ```

  before the main function.

  Here is a typical program run. The user input is printed in color.

  ```
  Hello, my name is Hal!
  What is your name?
  Dave
  Hello, Dave. I am glad to meet you!
  ```

- **P1.3** Write a program that prints your name in large letters, such as

  ```
  *   *   **   ****   ****   *   *
  *   *  *  *  *     *     *   *
  *****  *  *  ****  ****  *   *
  *   *  *  *  *     *     *   *
  *   *  *  *  ****  ****  *   *
  ```

- **P1.4** Write a program that prints a face similar to (but different from) the following:

  ```
  /////
  +-----+
  (| o o |)
  | , . |
  |-----|
  ```

- **P1.5** Write a program that prints a house that looks exactly like the following:

  ```
     /\
    /  \
   +----+
   | . .|
   | || |
   +----+
  ```

- **P1.6** Write a program that prints an animal speaking a greeting, similar to (but different from) the following:

  ```
     /\   /\
    ( ' ) / Hello \
    ( . ) < Junior |
      | | \ Coder!/
      (___)  -----
  ```

- **P1.7** Write a program that prints an imitation of a Piet Mondrian painting. (Search the Internet if you are not familiar with his paintings.) Use character sequences such as @@@ or ::: to indicate different colors, and use - and | to form lines.

- **P1.8** Write a program that prints the United States flag, using * and = characters.

- **Engineering P1.9** The atmospheres of the gas giant planets (Jupiter, Saturn, Uranus, and Neptune) are mostly comprised of hydrogen (H₂) followed by helium (He). The atmospheres of the terrestrial planets are mostly comprised of carbon dioxide (CO₂) followed by nitrogen (N₂) for Venus and Mars, and for Earth, mostly Nitrogen (N₂) followed by Oxygen (O₂). Write a program that outputs this information in a chart with four columns for the type of planet, the name of the planet, its primary atmospheric gas, and its secondary atmospheric gas.

  ![](img/d61019b035dd82beb581604273c0ee6b_62_0.png)

  © Courtesy NASA/JPL-Caltech.

- **Engineering P1.10** Write a program that displays the following image, using characters such as / \ | + for the lines. Write Ω as "Ohm".

  ![](img/d61019b035dd82beb581604273c0ee6b_62_1.png)
