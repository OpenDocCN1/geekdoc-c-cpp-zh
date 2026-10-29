
```
i = -50
For s in spheres do
(
    s.position = [i,i,i]
    i = i + 10
)
```

Study this script to make sure that you understand what's going on. You use a for loop to process each sphere in your collection of spheres. For each one, you set its position to [i, i, i], and then you change the value of i so that the next sphere is at a different location.

## Functions

The last feature of basic MAXScript that you'll look at is the function. Functions are small chunks of MAXScript that act like program building blocks. For example, suppose that you need to compute the average of a collection of numbers many times during a script you're writing. The MAXScript to do this might be:

```
Total = 0
Count = 0
For n in numbers do
(
    total = total + n
    count = count + 1
)
average = total / (count as float)
```

Given a collection of numbers called numbers, this MAXScript computes the average. Unfortunately, every time you need to compute the average, you have to type all that MAXScript again. Or you might be smart and just cut and paste it in each time you need it. Still, your script is quickly becoming large and ugly, and you always have to change the script to match the name of your collection you're averaging.

A function solves your problem. At the beginning of your script, you can define an average function like this:

```
Function average numbers =
    ( -- Function to average the numbers in a collection
    local Total = 0
    local Count = 0
    For n in numbers do
    (
        total = total + n
        count = count + 1
    )
    total / (count as float)
)
```

Now any time you need to average any collection of numbers in your script, you could just use this to take all the numbers in the collection called num and store their average in a variable called Ave:

```
Ave = average num      -- assuming num is a collection
```

Not only does this make your script much shorter if you need to average numbers often, but it makes it much more readable, too. It's very clear to the casual reader that you're going to average some numbers. Also, if you later realize that you wrote the average function incorrectly, you can just fix it at the top of the

## Part XII: MAXScript and Plug-Ins

script. If you weren't using functions, you would have to go through your script and find every case where you averaged numbers and then fix the problem. (What a headache!)

Now take another look at the function definition. The first line

```
Function average numbers =
```

tells Max that you're creating a new function called average. It also tells Max that to use this function, you have to pass in one piece of data, and that inside the function you refer to that data using a variable called numbers. It doesn't matter what the name of the actual variable was when the function was called; inside the function, you can simply refer to it as numbers.

Creating functions that use multiple pieces of data is also easy. For example,

```
Function multEm a b c = (a * b * c)
```

creates a function that multiplies three numbers together. To use this function to multiply three numbers and store the result in a variable called B, you would simply enter

```
B = multEm 2 3 4
```

The next two lines

```
local Total = 0
local Count = 0
```

create two variables and set them both to 0. The local keyword tells Max that the variable belongs to this function. No part of the script outside of the function can see this variable, and if there is a variable outside the function with the same name, changing the variable inside this function won't affect that variable outside the function. That way, you never have to worry about what other variables are in use when someone calls average; even if variables are in use that are named Total or Count, they won't be affected.

The last line

```
total / (count as float)
```

## Tutorial: Creating a school of fish

Let's look at an example that puts into practice some of the things you've learned in this chapter. In this multipart tutorial, you use MAXScript to create a small school of fish that follows the dummy object around a path.

## Part 1: Making the fish follow a path

In this part of the tutorial, you use MAXScript to move one of the fish along a path in the scene. To do this, follow these steps:

- 1. Open the Fish scene.max file from the Chap 49 directory on the DVD.
- This scene consists of two fish and a dummy object that follows a path. What you need to do is use MAXScript to create a small school of fish that follows the dummy object around the path.

- 2. Press F11 to open the MAXScript Listener window. In the window, choose File ⇨ New Script to open the MAXScript Editor window, and type the following script:

## Chapter 49: Automating with MAXScript

```
pathObj = $Dummy01
fishObj = $Fish1/FishBody
relPos = [0,-150,-50]   -- How close the fish is to the path

animate on
(
    for t = 1 to 100 do at time t
    (
        fishObj.position = pathObj.position + relPos
    )
)
```

3. Select the Camera01 viewport. Choose Tools-> Evaluate All (or press Ctrl+E) to evaluate all the MAXScript in the Editor window, right-click the Camera01 viewport to activate it, and click the Play Animation button.
The fish rigidly follows the dummy object's path. Figure 49.15 shows one frame of this animation.

# FIGURE 49.15

First attempt at making the fish follow a path

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1246_0.png)

Now you'll explain the MAXScript entered in the previous tutorial. The first few lines create some variables that the rest of the script uses. pathObj tells the name of the object that the fish will follow, and fishObj is the name of the fish's body. (Notice that you can reference parts of the group hierarchy by using the object name, a forward slash, and then a child part.) Why bother creating a variable for the fish object? After you get this first fish working, you want to apply the same script to another fish. All you have to do is rename Fish1 as Fish2, re-execute the script, and you're finished!

The script also creates a variable called relPos, which you use to refer to the relative position of the fish with respect to the dummy object. If you have several fish in the scene, you don’t want them all in the exact same spot, so this is an easy way to position each one.

The next block of MAXScript is new: You’re using the animate on construct. This tells Max to generate keyframes for your animation. It’s the same as if you had pressed Max’s Animation button, run our script, and then shut Animation off. So any MAXScript inside the animate on parentheses creates animation keyframes. These parentheses define a section of the script you call a block.

Inside the animation block, you have a loop that counts from 1 to 100 (corresponding to each frame of our animation). On the end of the loop line, you have at time t, which tells Max that for each time through the loop, you want all the variables to have whatever values they’ll have at that time. For example, if you want the fish to follow the dummy object, you have to know the position of the object at each point in time instead of just at the beginning; so each time through the loop, Max figures out for you where the dummy object will be.

Inside the loop, you set the fish’s object to be that of the dummy object (at that point in time) and then adjust the fish’s position by relPos.

## Part 2: Adding body rotation and tail animation

Next you’ll make that fish look a little more lifelike by animating its tail and having it rotate its body to actually follow the path. Also, you’ll add a little unpredictability to its motion so that when you add other fish, they aren’t exact copies of each other.

To improve the fish’s animation, follow these steps:

- 1. Type the revised version of the script (the new lines are in bold):

```
pathObj = $Dummy01
fishObj = $Fish1/FishBody
fishTail = $Fish1/FishBody/FishTail
relPos = [0,-150,-50]  -- How close the fish is to the path

fishTail.bend.axis = 0  -- 0 is the x-axis
zadd = 4  -- vertical movement at each step
tailFlapOffset = (random 0 100)
tailFlapRate = 25 + (random 0 25)
animate on
(
for t = 0 to 100 do at time t
(
fishObj.position = pathObj.position + relPos
fishObj.position.z = relPos.z
relPos.z += zadd

-- let’s say that there’s a 10% chance that the fish will
-- change directions vertically
if ((random 1 100) > 90) then
(
zadd = -zadd
)

fishTail.bend.angle = 50 * sin (t * tailFlapRate +
tailFlapOffset)
)
```
