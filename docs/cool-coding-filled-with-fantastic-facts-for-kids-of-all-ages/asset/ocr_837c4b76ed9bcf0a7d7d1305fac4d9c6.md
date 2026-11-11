![](bbox=[0.02, 0.01, 0.99, 0.56])

# **Reading things in**

Just as you can have a program write text out, you can have it read text in too! How precisely a program reads from the keyboard varies from language to language: you can read a single character (key press) at a time or a whole string until the user hits enter. Once you’ve done so, you can go ahead and store that input in a variable.

If you want your user to enter a number there's one more step. You see, to a computer the string “12” is different from the number 12; the first is a string just like “elephant” or “football”, not a number it understands. To change from a string into a number you need to tell the program to convert it: a function like int("12") will convert it to the integer 12, while float("12") will turn it into the floating point number 12.0.