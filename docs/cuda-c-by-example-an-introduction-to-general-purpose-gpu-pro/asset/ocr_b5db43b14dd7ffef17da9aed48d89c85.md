We know that OpenGL and the CUDA runtime will have different names for our GPU buffer, and we know that we will need to refer to both of these names, depending on whether we are making OpenGL or CUDA C calls. Therefore, our structure will store both OpenGLs bufferObj name and the CUDA runtime's resource name. Since we are dealing with a bitmap image that we intend to display, we know that the image will have a width and height to it.

To allow users of our GPUAnimBitmap to register for certain callback events, we will also store a void* pointer to arbitrary user data in dataBlock. Our class will never look at this data but will simply pass it back to any registered callback functions. The callbacks that a user may register are stored in fAnim, animExit, and clickDrag. The function fAnim() gets called in every call to glutIdleFunc(), and this function is responsible for producing the image data that will be rendered in the animation. The function animExit() will be called once, when the animation exits. This is where the user should implement cleanup code that needs to be executed when the animation ends. Finally, clickDrag(), an optional function, implements the user's response to mouse click/drag events. If the user registers this function, it gets called after every sequence of mouse button press, drag, and release events. The location of the initial mouse click in this sequence is stored in (dragStartX, dragStartY) so that the start and endpoints of the click/drag event can be passed to the user when the mouse button is released. This can be used to implement interactive animations that will impress your friends.

Initializing a GPUAnimBitmap follows the same sequence of code that we saw in our previous example. After stashing away arguments in the appropriate structure members, we start by querying the CUDA runtime for a suitable CUDA device:

```
GPUAnimBitmap( int w, int h, void *d ) {
    width = w;
    height = h;
    dataBlock = d;
    clickDrag = NULL;
}
```