# Using the NLA Editor

Now that we've discussed how to handle weapons so to speak, we'll continue on with discussing the NLA Editor. The NLA Editor is used to mix and blend Actions to create complex animations. Let's look at an example of creating a shoot while running animation. In Figs. 7.10 and 7.11, you can see the run and shoot animations that were created for Tater.

It's hard to tell from the images, but the shoot animation has no keys set on the legs. By clicking the plus sign in the Action Editor, I created a new Action that starts with the bones in position from the previous Action's pose as shown in Fig. 7.12. However, the keyframes are removed in the new Action. I then keyframed a shooting animation and renamed this action to shoot.

Using the NLA Editor, you can then work with your animations as strips as they're called. It's much like using a video editor in that you can add strips or clips to a track and bend and transition between them. In our case, we just want to layer the shooting animation over the run, and this is done by placing the shoot track above the run and changing its blending mode to Add as shown in Fig. 7.13.

![](bbox=[0.12, 0.49, 0.96, 0.93])