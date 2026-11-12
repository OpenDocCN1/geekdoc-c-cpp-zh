
## ANIMATE THE DOG

I think it's finally time to bring the dog to life, don't you? Design an awake costume for Woof:

- 1. Shift-click Woof's sleeping costume and choose Duplicate.
- 2. Rename the costume Wake.
- 3. Click the Select tool.
- 4. Click and drag the dog's head up a bit (or you can use the Up Arrow key for a more precise movement).
- 5. Click and drag to rotate the tail up.

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_33_0.png)

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_33_1.png)

## ADD CODE TO ANIMATE THE STICK DOG

Timing is essential in animation, especially when you have two or more characters interacting. Can you figure out how many seconds the dog should wait until waking up? Look back at the code on *Sticky*: three seconds to glide in and then a one-second pause before starting the jumping jacks. So the dog should wait about five seconds, right?

- 1. Click the Scripts tab.
- 2. If you duplicated the stick figure sprite to make the dog as I did, the tab will already contain jumping jack code. Shift-click the `WHEN GREEN FLAG CLICKED` block and choose Delete.

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_33_2.png)

- 3. **Drag the following code blocks to the Scripts Area and change the values to match:**

```scratch
when green flag clicked
switch costume to sleep
wait 5 secs
switch costume to wake
```

Click the Green Flag button and the dog should sleep for five seconds, and then appear to wake up by lifting its head and tail. What might the dog do next? When I enter a room that has a dog, it usually starts wagging its tail.

## ANIMATE TAIL WAGGING

For a quick tail wag, duplicate the Wake costume, rename the new costume **Wag**, and use the Select tool to rotate the tail.

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_34_0.png)

Use a REPEAT block to switch between the Wake and Wag costumes. I think we also should add a two-second delay between the dog first waking and then wagging its tail. (Surely dogs need a few seconds between waking and showing excitement.)

```scratch
when green flag clicked
switch costume to [sleep v]
wait 2 secs
switch costume to [wake v]
wait 2 secs
repeat 3
    switch costume to [wag v]
    wait 0.25 secs
    switch costume to [wake v]
    wait 0.25 secs
```

## TALK LIKE A MAN

The characters are stick figures, so I think it works best to “stick” (pretty hilarious, right?) to speech bubbles, rather than recorded sounds and voices. (You use digital audio in Project 4.) You could draw a speech bubble into a new costume or make a separate sprite, but I find using the SAY blocks easier.

I want my figure to speak WHILE doing jumping jacks. If I put a SAY block inside the REPEAT block, Sticky will keep saying the same thing over and over until the last jumping jack is finished.

What is a poor little animator to do?

Scratch can have different chunks of code running at the same time on different sprites and even within the same sprite. This means you can keep your current gliding and jumping jacks code blocks on the stick figure, add a second WHEN GREEN FLAG

## 总体国家安全观

国家安全是指国家政权、主权、统一和领土完整、人民福祉、经济社会可持续发展和国家其他重大利益相对处于没有危险和不受内外威胁的状态，以及保障持续安全状态的能力。

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_36_0.png)

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_37_0.png)

## PROJECT 2 ANIMATE GREAT CHARACTERS

ENOUGH WITH STICK PEOPLE! In this project, you create a unique cast of characters by using vector-drawing tools and then you learn a few design techniques to help bring them to life.

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_38_0.png)

### KEEP IT SIMPLE, STUPID

When I was younger, I learned that KISS means more than just smacking your lips into somebody. It can stand for Keep It Simple, Stupid. The more complex your characters are, the harder it is to animate them. So keep your character design simple, dummy!

... draw a simple line for a mouth ...

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_40_0.png)

... and then fill each face with a different color:

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_40_1.png)

Wow, I don't know what you see, but I see a zombie, a person, and a werewolf!

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_40_2.png)

To keep it simple, I will create a story that involves these three characters and explore ways to bring the characters and their world to life.

### GETTING A HEAD START

Before starting, take a moment to think about the story you want to tell and the characters who would be the most fun to bring to life. If you don't have a good idea yet, don't worry, you can start messing around with a few characters and see where they lead you.

### CREATE A NEW PROJECT

- 1. Go to scratch.mit.edu or open the Scratch 2 Offline Editor.
- 2. If you are online, click Create. If offline, choose File > New.
- 3. Name your project. (Online, select the title and type Animation Characters. Offline, choose File > Save As and type Animation Characters.)
- 4. Delete the cat!

### PAINT A NEW SPRITE

- 1. Click the Paint New Sprite icon.
- 2. Click the Costumes tab.
- 3. Click the Convert to Vector button.
- 4. Click the Ellipse tool.
- 5. Click the Outline option.
- 6. Choose the black color swatch.
- 7. Click and drag to draw a head and two eyes.  
  You can hold down the Shift key to draw a perfect circle.
- 8. Draw two more ellipses for eye pupils.

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_41_0.png)

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_42_0.png)

If you want your eyes to be exactly the same size, use the Duplicate tool to make exact copies.

Is your character beginning to emerge? If not, perhaps a bit of hair will help.

### QUICK HAIRSTYLING

You can draw hair with the Pencil tool or sculpt it by using the Reshape tool on an ellipse or a rectangle. I will combine techniques to get a unique hairstyle for my zombie:

- 1. Click the Ellipse tool.
- 2. Click the Solid option.
- 3. Choose a color swatch for your hair color.
- 4. Click and drag right over your character’s face.
- 5. Shift-click the Back a Layer button to send the hair to the bottom layer (behind the head and eyes).
- 6. Click the Reshape tool.
- 7. Click the hair to select it.
- 8. Click and drag control points to style your hair.

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_42_1.png)

The Pencil tool is better at drawing jagged shapes, like zombie hair bangs!

- 1. Click the Pencil tool.
- 2. Choose a color swatch.
- 4. **Click the Select tool, click the mouth, and then use the Line Width slider to adjust the line thickness.**

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_44_0.png)

### GIVE ’EM A NOSE JOB

Although some zombies may have lost a nose in their travels, I think my little ghoul could use a petite schnoz. Use the Pencil tool to draw the nose on yours and then use the Reshape tool to smooth it.

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_44_1.png)

Nose placement can affect your character as much as the location of the eyes and mouth, so you might want to try a few positions before you lock in your face for all eternity.

### A LITTLE BODY WORK

Having the body, arms, and legs as separate objects makes characters easier to animate.

- 1. **Click the Ellipse tool, choose your outline color, and then draw an oval the approximate size you want for the body.**

I’ll choose classic black for my outline color.

- 2. **Click the Color a Shape tool, choose a color for the character’s shirt or dress, and then click inside the initial body shape.**

- 3. Click the Reshape tool, click the body to select it, and then click and drag points into the shape that looks best to you.

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_45_0.png)

### ADD SIMPLE LEGS

You can use the Rectangle tool to draw the legs together, use the Reshape tool to taper them at the ankles, and then fill them in with the pants, tights, or zombie skin color of your choice.

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_45_1.png)

Something doesn’t look right. Oh yeah! I don’t want the zombie’s dress to be too short. Shift-click the Back a Layer button so the legs appear behind the body. Then draw an ellipse and reshape it into shoes.
