The result is shown in Figure 16.24.

![](bbox=[0.291, 0.127, 0.703, 0.503])

**Figure 16.24** A scene with three overlapping colored light sources, colors added together.

To most people new to color models, Figure 16.24 looks very strange (it looks even stranger with red/yellow/blue panes – try it!). The red and blue planes combine to form a sort of light purple called *magenta*, which probably seems fairly reasonable – but few people expect red and green would combine to make yellow. And yet, if these panes were *light sources*, believe it or not, this is much closer to what would actually happen in the real world. Note, for example, that at the very center, all three red/green/blue primary light colors have been added together, resulting in full spectrum white light. So the RGB additive color model, when used to blend colors by adding them, is accurate when we use it to blend colored light sources.

But what if we want to model colored objects that aren’t light sources, but are instead passive colored objects responding to white light sources, such as a colored window pane or a pair of orange sunglasses? It turns out that the additive RGB model is quite clumsy for this task.

If colored transparent objects are desired, rather than light sources, one option is to switch to a *subtractive* color model, such as CMY (cyan/magenta/yellow). Whereas RGB is designed for computer monitors composed of tiny red, blue, and green light emitters, CMY is commonly used for printers that mix ink to build