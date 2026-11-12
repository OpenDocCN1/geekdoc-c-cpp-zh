![](bbox=[0.33, 0.1, 0.96, 0.39])

**FIG 6.4** The Foot Bone is Used to Raise the Heel. Notice that its Direction Has Been Flipped.

![](bbox=[0.33, 0.41, 0.96, 0.67])

**FIG 6.5** The Knee Bone Allows You to Articulate the Tip of the Boot.

As you will see in the next section, setting up these controls for the feet and legs were actually a simple task, yet I'm getting a lot of articulation. These controls allow me to move the leg, animate toe taps, stomp the heel, and position the knees as well as when used together to help create a good articulation in run and walk cycles.

Next, let's take a look at the arms. The arms have an IK target as well. The Hand Bone is constrained to the IK target so that it drives the translation and rotation of the hand, and I can hide the actual Hand Bone. Basically by removing the Hand Bone as a control, I have one less control to worry about and a cleaner rig. I then have an elbow control, which is also a Pole Vector on the arms IK Constraint just as with the legs. This allows me to position the elbow as shown in Fig. 6.7.