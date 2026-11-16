# CHAPTER 4

![](bbox=[0.62, 0.12, 0.9, 0.38])

# TIME AND SPACE

When I was learning game programming, and I wanted to do something involving physics, I searched for some equations and read some tutorials about movement. I then tried to write some code involving gravity, and I tried to do it correctly, so that the gravity would be the same in my computer program as it is on earth. When I read that gravity is 9.8 m/s², I stopped, stared at the computer for a while, and didn’t have a clue where to start. I didn’t have anything like a meter, and no seconds. I was stumped. It was at this point that I began to realize how difficult computer games could be. The goal of this chapter is to add a timestep to the game loop, allowing for calculations involving time. It also covers screen mapping so any arbitrary coordinate system can be drawn on a window of any size.

# CALCULATING TIME DELTA

All of the previous examples have been updating the moving objects every frame. This causes different computer speeds to move objects faster or slower depending on the frame rate. See Figure 4.1.