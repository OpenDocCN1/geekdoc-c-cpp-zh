# CHAPTER 4: Making Decisions About...and Planning Flow

```
declare procedure run on class MyScene
do order
  Boolean keepPlaying = true
  while keepPlaying is true
    Integer randomNumber = nextRandomIntegerFromUpToIncluding(0, 100)
    this.primRobot say "The secret number is " + randomNumber; duration:2.0; more
    Boolean continueGuessing = true
    while continueGuessing is true
      Integer userGuess = this.astronaut getIntegerFromUser("Guess a number from 0 up to including 100?")
      if userGuess == randomNumber
        continueGuessing = false
        this.astronaut say "Correct Guess!"; duration:2.0; more
      else
        if userGuess > randomNumber
          this.astronaut say "Your guess was too high."; duration:2.0; more
          this.primRobot say "The user guessed: " + userGuess; more
        else
          this.astronaut say "The guess was low."; duration:2.0; more
          this.primRobot say "The user guessed: " + userGuess; more
    endwhile
    keepPlaying = this.astronaut getBooleanFromUser("Play again?")
end
```

**Figure 4-8.** Random number generator; complete program listing

Figure 4-8 shows the entire program listing for your random number generator code at forum.xcelme.com.

> NOTE: You can download the complete random number generator app at random number generator code. The code will be under the Chapter 4 topic. There is also a video showing how to drag and drop all the tiles within the While and If code blocks in Alice.

# # Coding the Example App in Objective-C

Using your requirements and what you learned with your Alice app, try writing your random number generator in Objective-C.

Your Objective-C app will run from the command line, as it asks the user to guess a random number.

+   1. Open Xcode and start a New Project. Choose the Command Line Tool. See Figure 4–9.