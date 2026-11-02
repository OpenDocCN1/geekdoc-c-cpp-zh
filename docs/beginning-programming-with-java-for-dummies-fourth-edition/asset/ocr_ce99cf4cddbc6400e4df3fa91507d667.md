Finding this @ sign would jump me out of the inner loop and back to the top of the outer loop, as shown in Figure 14-6.

# Figure 14-6:
Leaving the inner loop.

![](bbox=[0.27, 0.26, 0.84, 0.48])

I'd get the B in BurdBrain, and sail back into the inner loop. But then (horror of horrors!) I'd write that B to the usernames.txt file (see Figure 14-7).

# Figure 14-7:
The error of my ways.

![](bbox=[0.27, 0.6, 0.84, 0.78])

There's the error! You don't want to write host names to the usernames.txt file. When the computer found the @ sign, it should have skipped past the rest of John's e-mail address.

At this point, you have a choice. You can jump straight to the corrected code in Listing 14-3, or you can read on to find out about the error message in Figure 14-3.

# Why the computer accidentally pushes past the end of the file

Ah! You're wondering why Figure 14-3 has that nasty error message.