In this example, we make a game similar to hangman where we ask the user to guess the name of the country. We have a tuple of various country names. The user is allowed to have guess a few times incorrectly before losing. We make a list of correctly guessed characters where correct guesses are appended to. The user wins when the guessed list length is equal to country name length. Note that we used a list data structure for guessed characters since it is continuously updated while countries are in tuple since it is never mutated.

```
```python
# guess a random country

import random

# list of countries
countries = ('france', 'usa', 'spain', 'india', 'brazil', 'norway', 'germany')

# Choose random country from countries
country = random.choice(countries)

# number of turns
turns = 4

# a list to store the guessed characters
gessed = []
while turns > 0:

    # print guessed characters
    for char in country:
        if char in guessed:
            print(char, end='')
        else:
            print('_', end='')

    print()
    print(f"You have {turns} left.")

    # user input
    guess = input("I guess a character:")

    # make sure guess is lowercase
    guess.lower()
```
```