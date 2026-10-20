duced by a complex mathematical calculation. The calculation uses the current time of day (which, of course, changes constantly) to seed the random-number generator such that each execution of a program yields a different sequence of random values.

The range of values produced directly by method nextInt generally differs from the range of values required in a particular Java application. For example, a program that simulates coin tossing might require only 0 for “heads” and 1 for “tails.” A program that simulates the rolling of a six-sided die might require random integers in the range 1–6. A program that randomly predicts the next type of spaceship (out of four possibilities) that will fly across the horizon in a video game might require random integers in the range 1–4. For cases like these, class Random provides another version of method nextInt that receives an int argument and returns a value from 0 up to, but not including, the argument’s value. For example, for coin tossing, the following statement returns 0 or 1.

```
int randomValue = randomNumbers.nextInt( 2 );
```

# Rolling a Six-Sided Die

To demonstrate random numbers, let’s develop a program that simulates 20 rolls of a six-sided die and displays the value of each roll. We begin by using nextInt to produce random values in the range 0–5, as follows:

```
face = randomNumbers.nextInt( 6 );
```

The argument 6—called the scaling factor—represents the number of unique values that nextInt should produce (in this case six—0, 1, 2, 3, 4 and 5). This manipulation is called scaling the range of values produced by Random method nextInt.

A six-sided die has the numbers 1–6 on its faces, not 0–5. So we shift the range of numbers produced by adding a shifting value—in this case 1—to our previous result, as in

```
face = 1 + randomNumbers.nextInt( 6 );
```

The shifting value (1) specifies the first value in the desired range of random integers. The preceding statement assigns face a random integer in the range 1–6.

Figure 6.6 shows two sample outputs which confirm that the results of the preceding calculation are integers in the range 1–6, and that each run of the program can produce a different sequence of random numbers. Line 3 imports class Random from the java.util package. Line 9 creates the Random object randomNumbers to produce random values. Line 16 executes 20 times in a loop to roll the die. The if statement (lines 21–22) in the loop starts a new line of output after every five numbers.

```
1  // Fig. 6.6: RandomIntegers.java
2  // Shifted and scaled random integers.
3  import java.util.Random; // program uses class Random
4
5  public class RandomIntegers
6  {
7      public static void main( String[] args )
8      {
9          Random randomNumbers = new Random(); // random number generator
```

Fig. 6.6 | Shifted and scaled random integers. (Part 1 of 2.)