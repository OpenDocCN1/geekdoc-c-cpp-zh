of difficulty with some stages being much easier than others. Let's look at it this way, there's a big difference between programming an entire OS versus writing a script to rotate an object in your Unity iOS game. By that same token, there's a big difference in having to create a character rig for a feature film versus a rig that allows you to create simple run, jump, and shoot animations for your game. Yes, you want your game animations to look great and set your work apart, but you're also working with a limited number of bones and your focus is on keeping the overall broad feel of the motion versus capturing every single minute detail. The point is, your game rig, especially in regards to the iPhone and iPad, doesn't need to have hundreds of overly complex and sophisticated controls. In fact, the simpler your rig is the better. In Fig. 6.1, you can see the completed rig for Tater. In Tater's rig, there are four IK targets and four pole targets used to rotate the knees and elbows. As you can see in Fig. 6.1, there aren't many controls used to animate Tater.

![](bbox=[0.34, 0.4, 0.95, 0.77])

FIG. 6.1 In This Image, You Can See the Controls Used to Animate Tater. Notice that There Aren't Many Controls to Deal With.

Let's examine the controls for the rig. First, we'll start with the feet and legs, which have a total of five controls as shown in Fig. 6.2.

In the feet, I have the IK target for the legs. The Foot Controller allows me to pick up Tater's foot and rotate it at the ankle as shown in Fig. 6.3. The Foot Bone is setup to allow Tater to raise his heel as shown in Fig. 6.4. The Toe Bone is used to articulate the toes as shown in Fig. 6.5.

Finally, I have the knee controls, which allow me to point the knees as shown in Fig. 6.6. These controls are Pole Vectors set on the IK Constraint.