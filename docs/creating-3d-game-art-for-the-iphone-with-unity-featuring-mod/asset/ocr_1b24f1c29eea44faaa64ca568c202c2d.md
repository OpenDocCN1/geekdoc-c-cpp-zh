![](bbox=[0.058, 0.105, 0.664, 0.538])

FIG 9.24 By Disabling the Emit Parameter the Emitter Won't Automatically Generate Particles. The One Shot Parameter Will Only Emit the Particles Once.

Finally, in the Explosion Script, the Particle Emitter's Emit parameter is activated when the Add Explosion Force is called as shown in Fig. 9.25. Also, notice that the script references the Particle Emitter as a public variable, which is set in the Unity iOS Editor.

FIG 9.25 The Explosion Script References the Particle Emitter and Then Sets the Emit Parameter to True When the Collision Happens, i.e., the Target Is Shot.

![](bbox=[0.058, 0.64, 0.909, 0.92])