Fix this error by adding the missing package to `spago.dhall`.

Now run the program in a Terminal Window, i.e. NOT in VSCode's terminal since it doesn't support all ANSI codes, it should produce:

![](bbox=[0.322, 0.148, 0.677, 0.217])

Try it and see what you get. Your mileage may vary due to differing support for ANSI codes in Terminal. I'm run this on a Mac using `iTerm2`. If you are on a Mac and run this in the standard `Terminal`, it'll work but the bold won't be as obvious. In the VSCode Terminal, it looks like the non-bold.

Now, look at the code. Can you see any problems? Any place for future problems or improvements we can make?

If you cannot, I'll demonstrate what I see.

Change the code to be:

```
test :: Effect Unit
test = log $ chalk [ "red", "bold" ] "Test" <> chalk [ "red " ] "Test"
```

Can you see what I changed?

I added a space right after the second red. Can you imagine what's going to happen?

Try making this change and running your program and see if you're guess is right.

Your program should crash with a Stack Trace. Try it.

THIS IS A PROBLEM. We have to be careful that Javascript doesn't drag down our PureScript code.

We have a great language like PureScript with Type Safety and we're using `Strings`, which leaves us vulnerable to all the same problems we gladly left behind when we abandoned Javascript.

We should be leveraging the Type System to protect us from ourselves.

The first thing we could do is to create helper Functions so we didn't have to worry about mistyping: