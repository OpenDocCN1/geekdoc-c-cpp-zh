# Making your own music

Scratch has blocks that can be used to invent musical sounds. You have a whole orchestra of instruments to conduct, as well as a full drum kit. The length of each note is measured in beats.

This decides how low or high the pitch of a note is

```
play note [60] for [0.5] beats
```

Big numbers make a note longer. It can also be shorter than a beat, as shown here

```
set instrument to [1]
```

Click here to choose an instrument from a drop-down menu

```
play drum [1] for [0.25] beats
```

```
rest for [0.25] beats
```

Use this menu to choose between different types of drum

This block adds a silent break in the music. Higher numbers will give you a longer break

# Playing music

# EXPERT TIPS

Connecting notes makes a tune. Create a variable called "note" (see pages 50–51), and then add the script below to sprite to create a piece of music.

# Tempo

The speed of music is called its tempo. The tempo decides how long a beat is within a piece of music. There are three blocks for managing the tempo.

```
when [clicked]
set [note] to [1]
set [instrument] to [1]
forever:
  choose an instrument
set [tempo] to [60] bpm
Add a "forever" loop around these two blocks
change [note] by [1]
play note [note] for [0.5] beats
```

The value of the variable "note" first

The tempo is measured in beats per minute, or "bpm."

Increase the tempo to make your music faster, or use a negative to make it slower.

```
change tempo by [60]
```

```
tempo
```

Checking this box makes the sprite's tempo show on the stage.

+   - Rising scale
This script makes a series of notes that play when the green flag is clicked. The pitch of each note gets one step higher at a time, and each note plays for a beat.

* Next