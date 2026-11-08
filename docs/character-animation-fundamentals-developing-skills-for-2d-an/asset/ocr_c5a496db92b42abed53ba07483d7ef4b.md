To do the blink, you will need to select the nodes ‘righttopeyelid’, ‘rightbotteyelid’, ‘lefttopeyelid’ and ‘leftbotteyelid’. They are in the middle of the tall hierarchy in the Hypergraph.

On the Time Slider delete (right click on each key frame or select the keys in the Graph Editor and press Delete) all the key frames apart from frames 1 and 100. With the four eyelid nodes still selected, set a rotation key frame at frame 23. Set a key at frame 25 and a key frame at 67.

We now need to set a key at frame 27 with the eyelids closed. Select the ‘righttopeyelid’ node and in the Channel Box type −80 in **Rotate in Z**. This will make the top eyelid shut. Set a rotation key. (Then open the eye settings for the rotation in Z are 0 for the top eyelids and 50 for the bottom eyelids.)

Repeat the same process for ‘lefttopeyelid’ and set a key. Then select ‘rightbotteyelid’; change the rotation in Z to 80 and set a key. Repeat this process for ‘leftbotteyelid’. If you play back your animation you will find that your eyes close quickly between frames 25 and 27 and open very slowly between frames 27 and 67. In order to keep the man’s eyes shut we need to set a key at frame 66 with the eyes shut. Select frame 66 in the Time Slider, repeat the process above to close his eyes and set a key. His eyes will now close at frame 27 and pop open at frame 67. Hopefully you will now have something like ‘litt_3D.avi’, in Chapter 3 on the website.

![](bbox=[0.442, 0.283, 0.976, 0.569])

# *The Lift Exercise in 3D Studio Max*

Copy the folder ‘maxman’ onto the C: drive of your computer (or wherever you want to put it). Open up 3D Studio Max, go to the main menu and select **File > Open**. Find ‘maxman.max’, which is in the ‘maxman’ folder. Highlight it and click the **Open** button.

Click the **Time Configuration** button and in the window that comes up have the **Frame Rate** set to ‘PAL 25fps’ (if you

![](bbox=[0.418, 0.598, 0.978, 0.921])