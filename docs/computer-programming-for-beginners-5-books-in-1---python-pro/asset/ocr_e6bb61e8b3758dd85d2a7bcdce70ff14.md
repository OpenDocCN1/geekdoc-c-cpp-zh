You can see how this presents the programmer with a much easier way to group important data together. There’s a good chance you aren’t going to be using this data *super* often, but it does allow you to have such a way to *do this*. It is important that you know what it is because you will eventually see it.

All of these concepts are important to Arduino because Arduino is far more restricted in terms of memory and processing power than your home computer would be. It is important that you know how to use these concepts so that you can make the most out of your Arduino’s processing ability as well as write simpler and more elegant sketches than you would have otherwise. For example, you could create a structure that held three-byte variables called r, g, and b in order to program your RGB colors alongside the same lines in a simple manner. You could define new colors doing this to access them easily later on in your program, like so:

```
struct color {

byte r, g, b;

};

color blue = {0, 0, 255};
```

See how simple that is? But the utility of doing such a thing is pretty plainly obvious!

In this chapter, we’ve covered three major programming concepts that you’re going to inevitably come across when you’re working with other people’s Arduino code and learning from what they’ve written, so it was important that I develop your ability to parse and work with these ideas.