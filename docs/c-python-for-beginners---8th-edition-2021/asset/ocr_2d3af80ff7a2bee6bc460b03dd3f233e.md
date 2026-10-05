# STEP 5

You don't always have to include quoted text within the input command. For example, you can ask the user's name, and have the input in the line below:

```
print("Hello. What's your name?")
name=input()
```

![](bbox=[0.068, 0.225, 0.485, 0.335])

```
Edit File Format Run Options Windows Help
print("Hello. What's your name?")
name=input()
```

# STEP 8

What you've created here is a condition, which we will cover soon. In short, we're using the input from user and measuring it against a condition. So, if the user enters David as their name, the guard will allow them to pass unharmed. Else, if they enter a name other than David, the guard challenges them to a fight.

![](bbox=[0.515, 0.225, 0.932, 0.335])

```
Edit File Format Run Options Windows Help
print("Hello. What's your name?")
name=input()
```

# STEP 6

The code from the previous step is often criticized as being a little nessa than having a lengthy amount of text in the input command, but it's not a rule that's set in stone, so do you like in these situations. Expanding the code, this:

```
print("Wait who goes there?")
name=input()
```

![](bbox=[0.068, 0.535, 0.485, 0.645])

```
Edit File Format Run Options Windows Help
print("Wait who goes there?")
name=input()
```

# STEP 9

Just as you learned previously, any input from is automatically a string, so you need to apply TypeCast in order to turn it into something else. This creates interesting aspects to the input command. For example:

# Code to calculate rate and distance

```
print("Input a rate and a distance")
rate=float(input("Rate: "))
```

![](bbox=[0.515, 0.555, 0.932, 0.665])

```
Edit File Format Run Options Windows Help
# Code to calculate rate and distance
print("Input a rate and a distance")
rate=float(input("Rate: "))
```

# STEP 7

It's a good start to take a text adventure game, perhaps?
Now you can expand it and use the raw input
to to flesh out the guard a little:

```
if name=="David":
print("Welcome, good sir. You may pass.")
else:
print("I know not you. Prepare for battle!")
```

![](bbox=[0.068, 0.965, 0.485, 1.0])

```
Edit File Format Run Options Windows Help
print("Wait who goes there?")
if name=="David":
print("Welcome, good sir. You may pass.")
else:
print("I know not you. Prepare for battle!")
```

# STEP 10

To finalise the rate and distance, we can add:
distance = float(input("Distance: "))
print("Time: ", (distance / rate))

Save and execute the code and enter numbers. Using the
float element, we do ensure that anything entered is
a floating number rather than a string.

![](bbox=[0.515, 0.965, 0.932, 1.0])

```
Edit File Format Run Options Windows Help
# Code to calculate rate and distance
print("Input a rate and a distance")
rate=float(input("Rate: "))
```