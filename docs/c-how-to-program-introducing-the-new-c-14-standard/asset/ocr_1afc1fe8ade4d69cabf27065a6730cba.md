To run the executable file `GuessNumber`, type `./GuessNumber` at the next prompt, then press *Enter* (Fig. 1.22). The `./` tells Linux to run from the current directory and is required to indicate that `GuessNumber` is an executable file.

```
```text
~/examples/ch01$ ./GuessNumber
I have a number between 1 and 1000.
Can you guess my number?
Please type your first guess.
?
```
```

Fig. 1.22 Running the GuessNumber application.

# Step 4: Entering Your First Guess

The application displays `"Please type your first guess."`, then displays a question mark (`?`) as a prompt on the next line (Fig. 1.22). At the prompt, enter `500` (Fig. 1.23). [Note that the outputs may vary based on the compiler you’re using.]

```
```text
~/examples/ch01$ ./GuessNumber
I have a number between 1 and 1000.
Can you guess my number?
Please type your first guess.
? 500
Too high. Try again.
?
```
```

Fig. 1.23 Entering an initial guess.

# Step 5: Entering Another Guess