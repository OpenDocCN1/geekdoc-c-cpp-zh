Now you can try your program, and you will find that it works, but it really isn't better than before. Our revised procedure square requires an input and gets an input, but it doesn't actually use it for anything!

Let's fix square that it makes use of the variable length. We want the value stored in length to be used as the input to forward. Do you remember how? Take a minute to think about it.

Instead of saying forward 50, we'll say forward what's in length. Instead of "what's in," use a colon before the variable. Change your square procedure as follows:

```
to square :length
repeat 4
[forward :length right 90 wait 1]
end
```

Now, to find input for forward, Logo must find the value stored in length. Where did that value come from? The value is stored there when Main calls the procedure square using a number.

Play with your new, more powerful square by changing this calling value, currently 30. Officially this value is called an argument. (I don't know why. I'm not mad; are you mad?) Inside the procedure variable is called a parameter.

You can also call square directly from the Command Center, for example by typing square 200 and now pressing Enter.

We have now finished a very good procedure that we can use any time we want. Here is my finished program, complete with lines setting off Main from the rest of the program, and procedures in alphabetical order:

```
to Main
cc
talkto "t1"
setsh [horse1 horse2 horse3]
repeat 20 [square 30]
end
```

```
to square :length
repeat 4
[forward :length right 90 wait 1]
end
```

```
to Start
Main
end
```

# Exercises