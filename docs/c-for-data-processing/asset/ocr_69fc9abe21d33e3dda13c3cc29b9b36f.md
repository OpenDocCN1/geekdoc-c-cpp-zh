The method above is from a ChildAccount class. This class extends the CustomerAccount and holds the name of the child's parent. The code above uses the ToString method in the parent object and then tucks the name of the parent on the end before returning it. The nice thing about this is that if the behaviour of the parent class changes, i.e. new members are added or the format of the string changes, the ChildAccount class does not have to change, since it will just make use of the upgraded method.

# 4.10.2 Objects and testing for equals

We have seen that when object references are compared a test for equals does not mean the same as it does for values. We know that objects are managed by named tags which refer to unnamed items held in memory somewhere. When we perform an equals test the system simply checks to see if both references refer to the same location.

To see how this might cause us problems we need to consider how we would implement a graphical computer game (makes a change from the bank for a while). In the game the various objects in it will be located at a particular place on the screen. We can express this position as a coordinate or point, with an x value and a y value. We then might want to test to see if two items have collided.

```
class Point
{
    public int x;
    public int y;
}
```

This is my point class. I can now create instances of Point and use them to manage my game objects:

```
Point spaceshipPosition = new Point();
spaceshipPosition.x = 1;
spaceshipPosition.y = 2;

Point missilePosition = new Point();
missilePosition.x = 1;
missilePosition.y = 2;

if ( spaceshipPosition == missilePosition )
{
    Console.WriteLine("Bang");
}
```

Note that I've made the x and y members of the Point class public. This is because I'm not that concerned about protecting them, but I do want my program to run quickly.

The problem is that the above program code does not work. Even though I have put the spaceship and the missile at the same place on the screen the word Bang is not printed.

This is because although the two Point objects hold the same data, they are not located at the same address in memory, which means that the equals test will fail.

# Programmer's Point: Make sure you use the right equals

As a programmer I must remember that when I'm comparing objects to see if they contain the same data I need to use the Equals method rather than the == operator. Some of the nastiest bugs that I've had to fix have revolved around programmers who have forgotten which test to use. If you find that things that contain the same data are not being compared correctly, take a look at the test that is being performed.

# Adding your own Equals method

The way that you solve this problem is to provide a method which can be used to compare the two points and see if they refer to the same place. To do this we must override the standard Equals behaviour and add one of our own: