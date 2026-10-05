# Unity Games by Tutorials

The canvas is indicated by a giant white box — and you'll notice that it's huge!

![](bbox=[0.346, 0.127, 0.653, 0.237])

This is because the canvas is assuming one pixel of screen space to be one unit inside of Unity. The canvas pixel density can be changed using the **canvas scaler**.

![](bbox=[0.331, 0.303, 0.668, 0.372])

The scaler has a property **UI Scale Mode** with some interesting options.

+   - **Constant Pixel Size** means the UI elements are the same size, regardless of screen size.

+   - **Scale with Screen Size** means UI elements grow bigger with the screen.

+   - **Constant Physical Size** means the UI elements will always be the same size, regardless of screen size or resolution.

This one component determines how your UI will look on different screen sizes and resolutions. For the purposes of this chapter, you'll be using the default values. Although the canvas shares the same space, you can effectively ignore it. Like any other GameObject, you can always deactivate it to maintain a clear "desk space," to speak.

An Image is a UI class of objects that lets you render an image on the screen via a **Sprite**. **Text**, quite logically, lets you render text on the screen. **Button** lets you configure hover and click events. You'll use these throughout this tutorial.

So you may be wondering, how are controls placed? Unity uses **anchors** and they look like arrows pointing at each other.