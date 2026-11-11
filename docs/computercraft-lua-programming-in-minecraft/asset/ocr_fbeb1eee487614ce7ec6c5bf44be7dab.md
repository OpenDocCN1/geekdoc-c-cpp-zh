will be displayed as `*s`. Note that this is a ComputerCraft specific feature, so if you try it on Lua not running in ComputerCraft, then it probably will not work.

```
```lua
if password == "password" then
```
```

..will look at the variable password which is what we typed in, and == means it will compare it to whatever we put on the other side, which is the text "password". This means that if you want to change the password, you have to change what's inside the quotes. The command then finishes the line off, so if what you typed in matches what is inside the quotes(your password) then it will do something.

There is another indent here to show that it is inside the *if* statement.

```
```lua
rs.setOutput("left", true)
```
```

..is saying that Redstone is turned on on the left side of the computer, which goes through the block, and triggers the door.

```
```lua
sleep(3)
```
```

..makes the computer wait 3 seconds before it moves on, and then `rs.setOutput("left", false)` turns off the Redstone signal on the left of the computer, therefore closing the door. I personally find keeping the door open for 3 seconds about right, but you can change it to anything you want.

Finally, the first *end* marks the end point of what the *if* statement should do, with *then* as the beginning point, and the second *end* is marking where the *while true do* loop should stop.

As this program is only 11 lines long, you can easily type it out, but, for example, it would be very tedious to type out the next program, so you can also refer to Appendix A for instructions on downloading all the Lua programs in this book.

# ## Summary

This is a nice simple project to get you started. There are a number of ways you could make this more sophisticated, by adding a maximum number of tries, or adding some options to change the password without having to edit the program.

Experiment and have fun, before you move on to the next project, which is a much more complicated program.