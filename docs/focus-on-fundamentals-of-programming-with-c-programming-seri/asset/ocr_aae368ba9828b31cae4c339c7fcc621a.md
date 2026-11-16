# Almost finished.

We are almost finished refining our algorithm. Let's put it all together and see how it looks.

```
// stepwise4
1. Find the length of the largest increasing sub sequence.
   1.1 Find the next increasing sub sequence.
       1.1.1. Examine the CURRENT_NUMBER.
       1.1.2. Compare the CURRENT_NUMBER to the PREVIOUS_NUMBER.
       1.1.3. if CURRENT_NUMBER is greater than the PREVIOUS_NUMBER
           then
           1.1.3.1. Add 1 to the LENGTH_OF_CURRENT_SUB_SEQUENCE.
       1.1.4. Let CURRENT_NUMBER now be called PREVIOUS_NUMBER.
       1.1.5. Let the next number now be the CURRENT_NUMBER.
       1.1.6. Repeat steps 1.1.2 through 1.1.5 until CURRENT_NUMBER is
           not greater than PREVIOUS_NUMBER.
   1.2. Compare the length of it to the GREATEST_LENGTH_SO_FAR.
   1.3. Call the longer of the two the GREATEST_LENGTH_SO_FAR.
   1.4. Repeat step 1.1 through 1.3 until finished.
2. Print the GREATEST_LENGTH_SO_FAR.
```

# A few words about variables, counting and initialization.

Don't be put off by unfamiliar names for some relatively simple concepts. A
variable is no more than the name of something. It is a way of referring to some
value that will vary over the course of an algorithm or program. For example, as
we look at one number at a time in an original sequence of numbers, whichever
number we are looking at right now: we call CURRENT_NUMBER.

CURRENT_NUMBER is the name of the variable that holds the value of the number
we are currently looking at. This allows us to create an algorithm that will work for
any sequence of numbers that meet the original description, not just one specific
sequence of numbers.