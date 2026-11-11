```
```lua
fails = 0
while fails < 5 do
    password = io.read()
    if password == "computercraft" then
        print("Opening Door")
    else
        print("Wrong Password")
        fails = fails + 1
    end
end
print("You are only allowed 5 attempts. Exiting")
```
```

Now, we are using a variable called fails that counts the number of times an incorrect password was entered. When this exceeds 5, the condition for staying in the while loop (that fails is less than 5) is no longer true and Lua exits the while loop and prints the message that the number of attempts has been exceeded.

This kind of "while" loop is handy if you just want to keep doing something until a condition stops being true. The other common situation where you might want to loop a certain number of times is called the "for" loop.

The following example prints out the numbers 1 to 10. Try typing it into a program (call it "fortest") and run it.

```
```lua
for i = 1, 10 do
    print(i)
end
```
```

Try changing 10 to 100 and run it again.

# ## Functions

When you write programs in any language, if you are not careful, there comes a point where everything gets too complicated to work out what is going on. A great way to keeps things simple and easy to modify is to break up your programs into manageable chunks called functions.

By putting sections of code in a function, you get the added advantage that you do not have to repeat yourself in your program, you can just call the same function from different places in your program.

There are really two things that you need to be able to do to a function. The first is to define it, which specifies the