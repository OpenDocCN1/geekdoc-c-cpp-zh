After the Skin modifier is applied and bound to the skin mesh, every bone includes an area of influence called an envelope that defines the skin vertices that it controls. If any of the skin mesh vertices are outside of the bone’s envelope or are included in an envelope for the wrong bone, then the vertices are left behind when the bone is moved. This causes an odd stretching of the skin that is easy to identify.

To check the envelopes, select and rotate several of the skeleton’s key bones. If any envelope problems exist, they are easy to spot, as shown in Figure 40.3. The incorrect stretching of the vertices for the boot simply means that the envelopes need to be adjusted.

# FIGURE 40.3

If the envelopes are off for any of the skin vertices, the skin stretches incorrectly.

![](bbox=[0.035, 0.46, 0.8, 0.83])

# Editing envelopes

When the Skin modifier is selected, the Parameters rollout includes an Edit Envelopes button that places you in a special mode that lets you edit the envelope for the selected bone in the bone list. This mode is also enabled by selecting the Envelope subobject under the Skin modifier at the top of the Modifier Stack.

When the Edit Envelopes mode is enabled, the entire skin mesh is colored with a gradient of colors to visually show the influence of the envelope. Areas of red are completely inside the envelope’s influence, areas of green are somewhat affected by the bone, and areas of gray are completely outside the envelope’s influence.

Figure 40.4 shows a simple loft object surrounding three bone objects with a Skin modifier applied. The Add Bone button was used to include the three bones within the Skin modifier list. The skin has been set to See Through in the Properties dialog box, so the bones are visible. The first bone was selected in the bone list, and the Edit Envelope button was clicked, revealing the envelope for the first bone.