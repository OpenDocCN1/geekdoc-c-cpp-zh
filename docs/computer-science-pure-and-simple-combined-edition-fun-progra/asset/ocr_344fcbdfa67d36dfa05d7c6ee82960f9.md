On the Graphics Page, drag the t2/pond out of the way and drag the t1/dog into the middle of the gray splotch. This should now make the Shape Center and be the pond is selected. Click on the first turtle, t1, look like the pond.

Our animation code will take care of making t2 look like a dog, if we change the code. Go to the Procedures Page. We need to change our talkto line so that we are now talking to t2. Change Main as shown:

+   to Main
cc
talkto "t2"
setsh [dog1 dog2]
seth 270
repeat 200
[Walk 10 10]
end

Give the program a try. There, that solves Problem 2. What do you think would be the way to solve Problem 1?

# Go the distance

I think we need to change our procedure doJump or to make a different procedure that both jumps up and forward. I like the first option of revising our existing procedure doJump and making it more flexible. We will try to make it so that it can be used both to jump up and down and jump over something.

To jump over an object, the turtle needs to move up and also move forward a certain amount. We need a second input to doJump so we can control how far forward the turtle should move while it is jumping. Let's think like:

+   We will need two variables or mailboxes to store two values, height and a new one—how about distance?
We'll set up a local variable, originalY, to hold the original y coordinate value.
We'll put the original y coordinate in there.
Now we'll set y to a new number, the sum of the old one and the value in height. We will wait a second.
Now we need to move forward to clear the pond. How about going forward by the amount stored in the variable/mailbox distance? Then wait a second.
Then set the y coordinate back to the original value.

Can you set up Logo code to match this line of reasoning? Try it. Then turn the page to mine, and see if yours is different.