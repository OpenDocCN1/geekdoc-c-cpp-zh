
To create bones, go to the Command Panel and select **Create > Systems > Object Type > Bones**. Alternatively, go to main menu and select **Animation > Create Bones** (or **Character > Bone Tools > Create Bones** in 3D Studio Max 5) and left-click in the scene. Press **Esc** to leave the mode.

To add an IK solver, select the top bone and in the main menu go to **Animation > IK Solver > HI Solver** and select the next bone but one.

To skin the bones, select the object to be skinned and from the main menu choose **Modifiers > Animation Modifiers > Skin**. In the Command Panel Parameters box under Edit Envelopes select the **Add Bone** button. Up will come the Select Bone window. Click the bones in the list that you want to be associated with your skin and click the **Select** button, and the bones will now move your skin very badly. To get something right, clicking the **Edit Envelopes** button and spend days trying to get the damn thing to move properly. Alternatively, parent an object to a bone (much easier).

## 11 Giving Your Characters Color in 3D Studio Max

Right-click on the object, click on **Properties**, click on the colored box next to **Name**, choose a color and then click **OK** twice.

## 12 Importing Sound into 3D Studio Max

Right-click on the Time Slider and select **Configure > Show Sound Track**. Go to the main menu and click **Graph Editors > Track View**. Click the **Function Curves** button at the top of the Track View in 3D Studio Max 4 or go to the main menu and select **Graph Editors > Track View > Open Track View – Curve Editor** in 3D Studio Max 5. Select **Sound** by right-clicking in the hierarchy tree and select **Properties** from the list that comes up. This will open the ProSound window. Select Add and from the **Open** window find your sound, select it and click **OK**. Click **OK** in the ProSound window and you should now have your sound in the hierarchy tree. It should also appear in the Time Slider and in the Track View. If you play back the Time Slider with the playback controls you will hear your sound playing.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_57_0.png)

## 13 Rendering Your Work in 3D Studio Max

Go to the main menu and select **Rendering > Render Setup** and up will come the **Render Setup** window.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_58_0.png)

Make sure you select the **Range** radio button and make sure the start and end frames are correct. Make sure your **Output Size** is correct (e.g. 768 × 576). In the **Render Output** section (you may have to scroll down to find this section) click **Files** and up will come the **Render Output File** window.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_59_0.png)

Give your movie a name in the **File name** box and choose how you want it to be saved in the **Save as type** box. If you choose **.avi** the program will ask you what codec to compress your .avi with. Close the **Render Output File** window. Click the **Render** button at the bottom of the **Render Scene** window. With any luck you should be rendering your scene!

## Overview of the ‘Ball Drop’ Exercise in 3D

Open up your 3D computer program and take out your ‘balldrop’ animation drawings and the related X-sheet (or look back at the illustration showing the eight drawings with timing charts). Create a ball. Make sure the Time Slider or Frame Slider is at the first frame and move the ball to a position similar to drawing 1 of your 2D animation. Set a key position. Then move the Frame/Time Slider to frame 9 and position the ball as in drawing number 9 (the second key position).

Copy each of the key positions from your animation onto the computer in this way and set keys at the key positions of your drawn animation.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_60_0.png)

Play back your animation (or have a look at 'ball_drop_keys_3D.avi', animations001, Chapter 1 on the website). It will look odd because of the way the program in-betweens the key positions. It does this by accelerating out of one key and decelerating into the next. In order to adjust this we need to manipulate the curves (called either 'animation curves' or 'function curves') that relate to the animation of the ball. In all 3D computer animation programs, the movement is broken down into a graph-like mathematical interpretation. If you take the up and down movement of the ball as the vertical value and the time it takes to do it as the horizontal value, you will end up with a series of points on a graph that correspond to where you have set your key frames. The computer program will join these points together to produce a curve and this will provide the in-between movement of your object. The default type of line linking the curves is called a 'spline'.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_60_1.png)

You can change the way the computer in-betweens your key positions by adjusting these curves. There are a number of different options. ‘Linear’ is a straight line between each key. A ‘stepped’ or ‘constant’ line continues at the same value as the first key before jumping to the value of the next key.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_61_0.png)

Linear Curves.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_61_1.png)

Constant or Stepped Curves.

The key points can also be given ‘handles’, making it possible to adjust the angle of the curve (Curves with handles can be called ‘Bezier splines’).

![](img/49afe0fca1d8f7ebd02f6839692b55f6_62_0.png)

![](img/49afe0fca1d8f7ebd02f6839692b55f6_62_1.png)

For our bouncy ball we need to ‘break’ the curve at the key position where the ball hits the ground. This means we need to make the curve ascend and descend between the keys in a nice parabola. From here we need to have a second parabola for the second bounce, a third parabola for the third bounce and so on.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_62_2.png)

Take a look at ‘ball_drop_3D.avi’ in animations001, Chapter 2 on the website. The ball is now bouncing more like a ball should!

Of course, I’m not suggesting that you should always start by working in 2D, but while you are learning to animate it will help you pick up timing all the quicker. By the end of the book you will only need to work out the basic key positions in 2D (in a very rough form) before animating in 3D.

## How to Animate a Basic Bouncy Ball in Maya

### How to Create Your Ball

Open up Maya and make the screen turn into four view panels by pressing the space bar on your keyboard quickly once. Make the mouse pointer hover over the front view panel and press the space bar quickly again to make the front view panel full screen.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_63_0.png)

![](img/49afe0fca1d8f7ebd02f6839692b55f6_63_1.png)

![](img/49afe0fca1d8f7ebd02f6839692b55f6_63_2.png)

To create a ball, go to the main menu and select **Create > NURBS Primitives > Sphere** (alternatively click the **Sphere** icon on the shelf above the view panel). Then click and drag in the view panel. This will create a ball.

You can rename your ball by going to the top of the **Channel Box** and under **SHAPES** clicking on ‘NURBSSphere1’ (the current name of your ball), which will turn blue. Type in a new name; let’s be imaginative and call it ‘ball’. Press Enter. The position of the ball can be controlled by typing in the upper part of the Channel Box. Next to **Translate X** and **Translate Y**, type ‘0’. This will bring the ball to the center of the viewport.

The size and shape of the ball can be altered by going to the **Inputs** section of the Channel Box and clicking on ‘MakeNurbSphere’. This will open a series of input boxes: **Radius** (the radius of the sphere) – type ‘1’ to give it a radius of 1 unit; **Start Sweep** and **End Sweep** (by adjusting the figures in these boxes you can end up with a sphere that looks a bit like an orange with a few segments missing); **Degree** (this will change the ball from the low-resolution look to the high-resolution look); **Sections** (this controls the number of lines running up and down the sphere); **Spans** (this controls the number of lines running from side to side across the sphere); and **Height Ratio** (I haven’t got a clue what this does so I keep it at 2).

Have a play at changing the inputs on the ball. If you mess up, delete it and create another. When you have adjusted the ball to something that you like, it’s always a good idea to delete its history. Do this by selecting the ball and from the main menu selecting **Edit > Delete by Type > History**. This sets the ball to the new shape.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_64_0.png)

### How to Animate Your Ball

Take out your drawn animation of a ball dropping (or have a look at the ball dropping illustration earlier in this chapter). Click the **Animation Preferences** button at the bottom right of the screen. Up will come the **Preferences** window. In the **Categories** box select **Settings** and in the box next to **Time** select ‘PAL (25 fps)’ (unless you are in a country that uses NTSC, in which case choose ‘NTSC (30 fps)’). Alternatively, keep it at 24 fps (film speed); this is easier to work with mathematically (it is more easily divisible than 25). Click **Save** to close the **Preferences** window.
