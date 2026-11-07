
```cpp
for (size_t row{0}; row < sales.size(); ++row) {
    for (size_t column{0}; column < sales[row].size(); ++column) {
        sales[row][column] = 0;
    }
}
```

### 6.10 (Random Sentences)

Write a program that uses random-number generation to compose sentences. Use four arrays of strings called *article*, *noun*, *verb* and *preposition*. Create a sentence by selecting a word at random from each array in the following order: *article*, *noun*, *verb*, *preposition*, *article* and *noun*. As each word is picked, concatenate it to the previous words in the sentence. Spaces should separate the words. When the final sentence is output, it should start with a capital letter and end with a period. The program should generate and display 20 sentences.

### 6.11 (Intro to Data Science: Coin Tossing)

Modify the die-rolling simulation in Section 6.10 to simulate the flipping of a coin. Use randomly generated 1s and 2s to represent heads and tails, respectively. Initially, do not include the frequencies and percentages above the bars. Then modify your code to include the frequencies and percentages. Run simulations for 200, 20,000 and 200,000 coin flips. Do you get approximately 50% heads and 50% tails? Do you see the “law of large numbers” in operation here?

### 6.12 (Intro to Data Science: Rolling Two Dice)

Write a program that simulates the rolling of two dice. The sum of the two values should then be calculated. [*Note:* Each die can show an integer value from 1 to 6, so the sum of the two values will vary from 2 to 12, with 7 being the most frequent sum and 2 and 12 being the least frequent sums.] The following diagram shows the 36 possible combinations of the two dice:

|   | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| 1 | 2 | 3 | 4 | 5 | 6 | 7 |
| 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| 5 | 6 | 7 | 8 | 9 | 10 | 11 |
| 6 | 7 | 8 | 9 | 10 | 11 | 12 |

If you roll the dice 36,000,000 times:

- The values 2 and 12 each occur 1/36th (2.778%) of the time, so you should expect about 1,000,000 of each.
- The values 3 and 11 each occur 2/36ths (5.556%) of the time, so you should expect about 2,000,000 of each, and so on.

Roll the two dice 36,000,000 times. Use a one-dimensional array to summarize the frequencies of each possible sum. Print the results in a tabular format. Also, determine if the totals are reasonable (i.e., there are six ways to roll a 7, so approximately one-sixth of all the rolls should be 7).

```cpp
constexpr size_t arraySize{10};
void someFunction(const std::array<int, arraySize>&, size_t); // prototype

int main() {
    std::array<int, 10> a{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    std::cout << "The values in the array are:\n";
    someFunction(a, 0);
    std::cout << '\n';
}

// What does this function do?
void someFunction(const std::array<int, arraySize>& b, size_t current) {
    if (current < b.size()) {
        someFunction(b, current + 1);
        std::cout << b[current] << ' ';
    }
}
```

### 6.17 (Sales Summary)

Use a two-dimensional array to solve the following problem. A company has four salespeople (1 to 4) who sell five different products (1 to 5). Once a day, each salesperson passes in a slip for each different type of product sold. Each slip contains:

- a) the salesperson number,
- b) the product number and
- c) the total monetary value of that product sold that day.

Thus, each salesperson submits 0 to 5 sales slips per day. Assume that the information from all the slips for last month is available. Write a program that will read all the information for last month’s sales (one salesperson’s data at a time) and summarize the total sales by salesperson by product. All totals should be stored in the two-dimensional array sales. After processing all the information for last month, print the results in a tabular format with each column representing a particular salesperson and each row representing a particular product. Cross total each row to get the total sales of each product for last month; cross total each column to get the total sales by salesperson for last month. Your tabular printout should include these cross totals to the right of the totaled rows and to the bottom of the totaled columns.

### 6.18 (Creating Three-Letter Strings from a Five-Letter Word)

Write a program that reads a five-letter word from the user and produces every possible three-letter string, based on the word’s letters. For example, the three-letter words produced from the word “bathe” include “ate,” “bat,” “bet,” “tab,” “hat,” “the” and “tea.”

### 6.19 (Telephone-Number Word Generator)

Standard telephone keypads contain the digits 0 through 9. The numbers 2 through 9 each have three letters associated with them, as is indicated by the following table:

| Digit | Letter | Digit | Letter |
|---|---|---|---|
| 2 | A B C | 6 | M N O |
| 3 | D E F | 7 | P Q R S |
| 4 | G H I | 8 | T U V |
| 5 | J K L | 9 | W X Y Z |

Fig. 6.15 Telephone digit-to-letter mappings.

Many people find it difficult to memorize phone numbers, so they use the correspondence between digits and letters to develop seven-letter words that correspond to their phone numbers. For example, a person whose telephone number is 686-2377 might use the correspondence indicated in the above table to develop the seven-letter word "NUMBERS."

Businesses frequently attempt to get telephone numbers that are easy for their clients to remember. If a business can advertise a simple word for its customers to dial, then no doubt the business will receive a few more calls. Each seven-letter word corresponds to exactly one seven-digit telephone number. The restaurant wishing to increase its take-home business could surely do so with the number 825-3688 (i.e., "TAKEOUT"). Each seven-digit phone number corresponds to many separate seven-letter words. Unfortunately, most of these represent unrecognizable juxtapositions of letters. It’s possible, however, that the owner of a barber shop would be pleased to know that the shop’s telephone number, 424-7288, corresponds to "HAIRCUT." A veterinarian with the phone number 738-2273 would be happy to know that the number corresponds to "PETCARE."

Write a program, given a seven-digit number, displays every possible seven-letter word corresponding to that number. There are 2187 (3 to the seventh power) such words. Avoid phone numbers with the digits 0 and 1.

- 6.20 (Functional-Style Programming: Cubing Integers) Use the techniques from Section 6.14 to calculate the cubes of the numbers 1–5.
- 6.21 (Functional-Style Programming: Summing the Triples of the Even Integers from 2 through 10) Use the techniques from Section 6.14 to calculate the total of the triples of the even integers from 2 through 10.
- 6.22 (Functional-Style Programming: Filtering and Mapping with an array) Create an array called numbers containing 1 through 15, then perform the following tasks and display the results:
  - a) Filter the elements of numbers, keeping only the even elements.
  - b) Map the elements of numbers to their squares.
  - c) Filter the elements of numbers, keeping only the even elements, then map them to their squares.
- 6.23 (Knight’s Tour: Intro to AI with Heuristic Programming) One of the more interesting puzzlers for chess buffs is the Knight’s Tour problem. The question is this: Can the chess piece called the knight move around an empty chessboard and touch each of the 64 squares once and only once? We study this intriguing problem in depth in this exercise.

  program to move the knight around the chessboard. Run the program. How many moves did the knight make?

  - c) After attempting to write and run a Knight's Tour program, you've probably developed some valuable insights. We'll use these to develop a heuristic (or strategy) for moving the knight. Heuristics do not guarantee success, but a carefully developed heuristic can significantly improve the chance of success. You may have observed that the outer squares are more troublesome than the squares nearer the center of the board. In fact, the most troublesome (or inaccessible) squares are the four corners.

    Intuition may suggest that you should attempt to move the knight to the most troublesome squares first and leave open those that are easiest to get to, so when the board gets congested near the end of the tour, there will be a greater chance of success.

    We may develop an “accessibility heuristic” by classifying each square according to how accessible it is, then always moving the knight to the least-accessible square (using the knight's L-shaped moves, of course). We label a two-dimensional array accessibility with numbers indicating how many squares are accessible from a particular square. On a blank chessboard, each center square is rated as 8, each corner square is rated as 2, and the other squares have accessibility numbers of 3, 4 or 6 as follows:

|   |   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|---|
| 2 | 3 | 4 | 4 | 4 | 4 | 3 | 2 |
| 3 | 4 | 6 | 6 | 6 | 6 | 4 | 3 |
| 4 | 6 | 8 | 8 | 8 | 8 | 6 | 4 |
| 4 | 6 | 8 | 8 | 8 | 8 | 6 | 4 |
| 4 | 6 | 8 | 8 | 8 | 8 | 6 | 4 |
| 4 | 6 | 8 | 8 | 8 | 8 | 6 | 4 |
| 3 | 4 | 6 | 6 | 6 | 6 | 4 | 3 |
| 2 | 3 | 4 | 4 | 4 | 4 | 3 | 2 |

    Now write a Knight's Tour program using the accessibility heuristic. At any time, the knight should move to the square with the lowest accessibility number. In case of a tie, choose any of the tied squares. Therefore, the tour may begin in any of the four corners. [Note: As the knight moves, your program should reduce the accessibility numbers as more and more squares become occupied. In this way, at any given time during the tour, each available square's accessibility number will remain equal to precisely the number of squares from which that square may be reached.] Run this version of your program. Did you get a full tour? Now modify the program to run 64 tours, one starting from each square of the chessboard. How many full tours did you get?

  - d) Write a version of the Knight's Tour program which, when encountering a tie between two or more squares, decides what square to choose by looking ahead to those squares reachable from the “tied” squares. Your program should move to the square where the next move would arrive at a square with the lowest accessibility number.

### 6.24 (Knight's Tour: Brute Force Approaches)

In Exercise 6.23, we developed a solution to the Knight's Tour problem. The approach used, called the “accessibility heuristic,” generates many solutions and executes efficiently.
