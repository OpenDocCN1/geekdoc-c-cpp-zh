
Now not all of these parameters must be expressed; however, if they are, they have to be laid out in the order listed there. So, for instance, the line of code:

```
Physics.Raycast (transform.position, transform.forward,
hit, 100);
```

means, “Cast a ray. As its origin, use the position of the object this script is attached to (transform.position). For the direction, cast the ray along the object’s Z-axis (transform.forward, which is really shorthand for “along the Z-axis”). Keep track of what we hit in the variable “hit” and cast the ray 100 units out—ignore everything further away than that.” That’s a lot of information in one line of script, no?

Now of course that line of script by itself is pretty useless. And in fact if it were just floating around in a script it would be fired once and therefore be pretty useless. However, if we told it to do that every frame we could start to gather a lot of information.

So consider the following function:

```
function Update () {
    var hit : RaycastHit;
    Physics.Raycast (transform.position, transform.forward, hit, 100);
}
```

function Update() just says, “do the things within the {} every frame.” var hit : RaycastHit just declares that we want to keep track of the RaycastHit with a variable called “hit.” Technically, this could go way up at a higher level and we could declare this variable at the top of the script, but since it is absolutely only going to be accessed within the raycasting mechanism, declaring the hit variable here helps keep relevant ideas together. Then comes the power line of code starting with Physics.Raycast. What this block of code is doing is always shooting out a ray that looks in the same direction as whatever this code is attached to (like a camera). The ray is keeping track of what it’s hitting (via the RaycastHit), which we can use later.

And all of that comes from that Scripting Reference. It may still be a little abstract here, so let’s get going in some tutorials to look at how to use this newfound knowledge.

## Tutorial 14.1: Highlighting Actionable Objects with Raycasting

The first tutorial we’re going to use raycasting for is to highlight an object that can be acted upon. Specifically, in this game we have a key that needs to be picked up and a power main switch that needs to be thrown. In games like this, it can be tough to know what items the player can actually do something to and which are there for visual fodder. Different games handle this in different ways, but a fairly consistent convention is to have the item glow, or change color, or otherwise highlight when the player moves his mouse or crosshairs over the item. This is the convention we are going to build.

Raycasting will do this really well. We'll set up a raycasting mechanism that shoots a ray from the camera and shoots it straight forward. When the center of the screen (where we will place a crosshairs) lines up on an object, the ray will strike it and let us know what the name of that object is. In the script we will compare the names of the objects the ray strikes with a list of actionable items; if it matches, we will turn up all the material's color values so that the item looks white hot. When the ray is not striking the object, the material will return to its regular color.

To do this, we'll need to make use of a crosshairs image. There is one included with the 2D Assets package imported in earlier tutorials (it's called Crosshairs) or you can make your own. The image should be a power of 2 in size (mine is 32x32) and have an alpha channel built into it in Photoshop.

We'll be doing these steps within the Scene-Hallway scene within Unity (continuing on from the last chapter).

- **Step 1**: Create crosshairs. Create a GUITexture to house the crosshairs (GameObject->Create Other->GUI Texture). Rename the GameObject Crosshairs. Use the Crosshairs image within the 2D Assets folder as the Texture for the GUITexture. If using the provided image, change the Pixel Inset X and Y to -16 and the Width and Height to 32.
- **Step 2**: Reduce the transparency of the crosshairs. With the Crosshairs GUITexture object selected, click the color swatch and reduce the Alpha (the A slider) to around 50 (Figure 14.5).

![](img/0285f88bc840f313779e011725b623a5_408_0.png)

**FIGURE 14.5** Setting up the crosshairs.

![](img/0285f88bc840f313779e011725b623a5_410_0.png)

FIGURE 14.6 Using Debug to check if the raycasting is working as anticipated.

## Tips and Tricks

Note that in Figure 14.6 the Collapse button is clicked in the Console. The script (as it now exists) is checking for the name of objects the ray is colliding with every single frame. This means that there will be 30 Debug.Log's per second (at least) showing up in the Console making it hard to read much of what's going on. The Collapse button collapses repeating warnings or Debug.Logs into one entry making it a bit easier to see what's happening down there.

## Why?

Why bother with these Debug thingies? True, true, Debug anything is most often used when trying to squash bugs, and in fact can be a very important part of trying to figure out if a script is going wrong and where it's going wrong. However, I find that using some basic Debug stuff early on in the process of developing a script helps me find out if the early drafts of the script are doing what I think they're doing. In fact, for some really elegant Debug stuff, try changing the last line to Debug.Log ("Selected object is " + hit.collider.gameObject.name);

- **Step 8**: Create an independent highlighting function. Further down from the function Update create a new function that reads thusly:

```
function Update () {
    var hit : RaycastHit;

    if (Physics.Raycast (transform.position, transform.forward, hit, 100)) {
        Debug.DrawLine (transform.position, hit.point);
        Debug.Log ("Selected object is " + hit.collider.gameObject.name);
    }
}

function AddHighlight(h10b:GameObject){
    h10b.renderer.material.color.r = h10b.renderer.material.color.r*10;
    h10b.renderer.material.color.g = h10b.renderer.material.color.g*10;
    h10b.renderer.material.color.b = h10b.renderer.material.color.b*10;
    yield WaitForSeconds (0.1);
    h10b.renderer.material.color.r = h10b.renderer.material.color.r/10;
    h10b.renderer.material.color.g = h10b.renderer.material.color.g/10;
    h10b.renderer.material.color.b = h10b.renderer.material.color.b/10;
}
```

## Why?

Lots to discuss here. First, what we're creating here is a new function that we can call on at other places within this script, or even call from other scripts. Of course, at this point we haven't called out to use this function quite yet, but we'll get to that in a bit. For now, let's look at what this script will do when it's called.

The first line simply creates a name for the new function (AddHighlight). But additionally, it declares a new variable that will be used just within this function (h10b:GameObject) but can be called to from other functions (h10b is just short for highlightObject and is a term I made up to use here—you could name it differently). Specifically, this means that when we call for this script we can call it for it and include what the GameObject is that this function will use for h10b. We're essentially allowing a variable of one function to be populated by another function elsewhere. Really powerful stuff.

Now below that, in the meat of the meal are lines that just say, "take the object to highlight, look in its renderer component, find the material, and then take whatever the red value is for the color of the material and multiply it by 10." Then do this for the green and blue values and the net results will be that the object highlights in bright white.

After that is a little trick that essentially says, "wait for 1/10th of a second, and then change it all back." The reason we're doing this is that we want to make sure that when the ray is no longer casting on the object to highlight, the object turns back to the way it was.

The function AddHighlight being separate means we can reuse this chunk of code multiple times without retyping it. We can start to develop mechanisms
