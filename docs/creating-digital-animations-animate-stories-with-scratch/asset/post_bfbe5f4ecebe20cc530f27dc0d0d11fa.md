
2. Drag and snap the SWITCH COSTUME TO, WAIT, and REPEAT blocks to the bottom of the other two blocks in the Scripts Area:

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_94_0.png)

I used the drop-down menu to choose Open in one SWITCH COSTUME TO block and Closed in the other. I also changed the WAIT time from the default 1 second to .25 second and the REPEAT value to 8. At the least, you will probably have to tweak the REPEAT value for your character. Can you figure out why?

When the Green Flag button is clicked, I want the mouth to open and close for as long as the audio plays. I didn't automatically know it would take 8 times of opening and closing to match the audio. The first time, I guessed 10. That was too long, so I tried 6, and then, finally, 8. You will have to adjust the value based on the length of your audio. You can also try different times for the WAIT block until you get the look you want.

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_94_1.png)

> If you do not use the WAIT blocks, the costumes will swap so fast you will not be able to see the costume change.

## ACHIEVE MORE REALISTIC LIP-SYNCHING

Go to a mirror, stand really close, fix your gaze on your mouth, and say the word donut as slowly as you can. Notice how not only your lips but also your teeth and even your tongue combine in different ways depending on which letters or sounds you are forming. For the *d*, your teeth start together and your tongue is at the roof of your mouth. When you get to *o*, your mouth is open and then it closes partway while your tongue bends up to the roof of your mouth for the *n*. Your mouth opens for the *u* and returns to the same position as the *n* for the *t*.

Don't worry: You do *not* have to draw every single letter of your dialogue (that would take forever!) Most people talk so fast you see only a few distinct mouth shapes. If you don't believe me, go back to that mirror and say, “I love donuts,” the way you normally speak.

The key to getting more realistic speaking animation is to animate the shapes the mouth makes at key times, otherwise known as *keyframes* (frames in which something important changes). Animators refer to the basic shapes your mouth makes to form the vowel and consonant sounds as *phonemes*. Although the English alphabet has 26 letters, there are far fewer phonemes because many letters overlap, such as M, P, and B (lips together) and D and T (tongue against upper teeth).

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_95_0.png)

So that you're on the same page as I am, let's all make our characters say, "I love donuts." (I mean, who *doesn't* love donuts?) I'm going to switch to Zomberta. Surely, zombies would love those gooey jelly donuts if they tried them.

1. **Click the sprite of the character who will be speaking, and then click the Sounds tab.**
2. **Click the Record New Sound button.**
3. **Rename the new sound object** Donuts.
4. **Click the Record button and say, "I love donuts."**
5. **Click the Stop button.**
6. **Select any silence at the beginning of your sound wave and choose Edit → Delete.**

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_96_0.png)

When your donut recording is ready, it is time to choose the key phonemes to add to your character. Here’s what I think will work best:

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_97_0.png)

See what I mean about duplicate phonemes (using #1 three times and #3 and #6 twice)? I did not create phonemes for the u or the t in *donuts*. Can you figure out why? The t and d are the same phoneme, and when I say *donuts*, the emphasis is on the first syllable (“DO-nuts”), so my mouth barely opens for the *u*.

## CREATE CUSTOM PHONEME COSTUMES

You need only phonemes 1, 3, 4, and 6 for your sentence. If you want to use your Mouth Open costume for #1, you need to create just two more mouth shapes:

1. Select the character you want to animate, and then click the Costumes tab.
2. Shift-click the Mouth Open costume and choose Duplicate.
3. Rename the new costume to correspond to the new phoneme mouth shape you are creating (such as “D/5/T/E”).
4. Use the Reshape tool to change the mouth to the desired phoneme shape.
5. Repeat Steps 2–4 for each remaining phoneme.

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_98_0.png)

*Wanna save yourself a ton of animation time? Why not make a new sprite named Talking, with each phoneme as a different costume. Then you can place that mouth over any character on the Stage. This trick will allow you to animate your character’s body separately from its mouth and then duplicate the sprite instead of creating a different set of phonemes for every character.*

After you create the phonemes you need, all that’s left is to synch them with the audio recording.

## SWITCH COSTUMES TO MATCH PHONEMES

Make sure you renamed all your costumes; otherwise, coding will be tricky:

1. Select the sprite containing the phoneme costumes.
2. Click the Scripts tab.
3. **Drag the following blocks into the Scripts Area:**

```
~~~scratch
when [green flag v] clicked
play sound [donuts v]
switch costume to [L, N, TH v]
wait (1) secs
~~~
```

4. **Shift-click the SWITCH COSTUME TO block, choose Duplicate, and drag and snap the copies to the bottom of the current blocks:**

```
~~~scratch
when [green flag v] clicked
play sound [donuts v]
switch costume to [L, N, TH v]
wait (1) secs
switch costume to [L, N, TH v]
wait (1) secs
~~~
```

5. **Repeat Step 4 until you have a SWITCH COSTUME TO block and a WAIT block for each phoneme.**

6. **Select the phoneme in each SWITCH COSTUME block.**

7. **Adjust the values of the WAIT block so the phoneme costumes come at the proper time while playing audio.**

My final script looks like this (I added red letters outside Scratch to show which blocks correspond to each part of my donuts audio):

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_100_0.png)

That final *M* shape closes the character's mouth when he or she has finished talking.

After you master the phonemes in *donuts*, you should be able to lip-sync all your animation characters. The key is finding the most important mouth shapes for any given word or phrase. And the faster your character talks, the fewer phonemes you should use. Otherwise, your character's mouth will be moving like crazy!

## MORE DIALOGUE TIPS

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_101_0.png)

- **Animate the jaw:** When you speak, it's not just about your lips, teeth, and tongue. Head back to the mirror and see where your jaw is when you go through the phonemes. It's easy to add: Just use the Reshape tool to tweak the bottom of the head.
- **Animate the eyes and eyebrows:** People tend to raise their eyebrows and open their eyes a bit wider when asking a question. What other ways can you change the eyes when a character speaks? (Your mirror beckons.)
- **Add blinking:** Unless your characters are in a staring contest, try adding an occasional blink to make them more realistic (or a wink to get them a date).
- **Animate hands:** Have you noticed how some people move their hands as they speak, almost as if they are conducting an orchestra (or trying to distract you while stealing your wallet)?
- **Try Audacity:** Audacity (audacity.sourceforge.net) is a free audio-editing application that gives you far more control over audio editing than you have with Scratch. Some of the biggest advantages are being able to zoom in to and out of your sound wave, show precise time information, speed up and slow down audio, and apply more sophisticated sound effects.

## PROJECT 5 LIGHTS, CAMERA, ACTION!

YOU HAVE COME UP WITH A STORY, CAST YOUR CHARACTERS, CREATED YOUR BACKDROPS, AND RECORDED SOME DIALOGUE.

Now it’s time to put all the elements together into an animation. The mix of design and programming tips in this project can streamline your animation process.

![](img/4bf9ba0253c33fcb16d2bd3d8eb1b121_102_0.png)

### (NOT) STARTING FROM SCRATCH

You should begin by opening a project that contains any characters, backdrops, or sounds (preferably all three) that you want to include in your animation. I’ll be using my characters, backdrops, and sounds throughout this project, while you should be using yours.

### CREATE A NIGHT SCENE

I want my first scene to be an interior of Hector’s apartment at night. But what if the character and backdrop I designed look like this?
