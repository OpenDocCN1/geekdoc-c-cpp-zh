
RGB value (1.0, 0.0, 0.0) yields pure red whether the maximum value of red is 255 (8 bits per color) or 65,535 (16 bits per color). However, the unsigned integer RGB value (255, 0, 0) yields pure red only if there are 8 bits per color. With 16 bits per color, (255, 0, 0) is nearly black.

Converting between these two representations is straightforward. Given an unsigned integer value, divide it by the maximum unsigned integer value to get the normalized value. Conversely, given a normalized decimal value, multiply it by the maximum unsigned integer value to get an unsigned integer value. For now, you should use unsigned integers because the SDL library expects them.

## Double Buffering

As mentioned earlier in this chapter, games update several times per second (at the common rates of 30 and 60 FPS). If a game updates the color buffer at the same rate, this gives the illusion of motion, much the way a flipbook appears to show an object in motion when you flip through the pages.

However, the refresh rate, or the frequency at which the display updates, may be different from the game’s frame rate. For example, most NTSC TV displays have a refresh rate of 59.94 Hz, meaning they refresh very slightly less than 60 times per second. However, some newer computer monitors support a 144 Hz refresh rate, which is more than twice as fast.

Furthermore, no current display technology can instantaneously update the entire screen at once. There always is some update order—whether row by row, column by column, in a checkerboard, and so on. Whatever update pattern the display uses, it takes some fraction of a second for the whole screen to update.

Suppose a game writes to the color buffer, and the display reads from that same color buffer. Because the timing of the game's frame rate may not directly match the monitor's refresh rate, it's very likely that the display will read from the color buffer while the game is writing to the buffer. This can be problematic.

For example, suppose the game writes the graphical data for frame A into the color buffer. The display then starts reading from the color buffer to show frame A on the screen. However, before the display finishes drawing frame A onto the screen, the game overwrites the color buffer with the graphical data for frame B. The display ends up showing part of frame A *and* part of frame B on the screen. Figure 1.3 illustrates this problem, known as **screen tearing**.

![](img/e9afcec1487716b0ef80d7e7c09869c8_91_0.png)

Figure 1.3 Simulation of screen tearing with a camera panning to the right

Eliminating screen tearing requires two changes. First, rather than having one color buffer that the game and display must share, you create two separate color buffers. Then the game and display alternate between the color buffers they use every frame. The idea is that with two separate buffers, the game can write to one (the **back buffer**) and, at the same time, the display can read from the other one (the **front buffer**). After the frame completes, the game and display swap their buffers. Due to the use of two color buffers, the name for this technique is **double buffering**.

As a more concrete example, consider the process shown in Figure 1.4. On frame A, the game writes its graphical output to buffer X, and the display draws buffer Y to the screen (which is empty). When this process completes, the game and display swap which buffers they use. Then on frame B, the game draws its graphical output to buffer Y, while the display shows buffer X on screen. On frame C, the game returns to buffer X, and the display returns to buffer Y. This swapping between the two buffers continues until the game program closes.

![](img/e9afcec1487716b0ef80d7e7c09869c8_92_0.png)

Figure 1.4 Double buffering involves swapping the buffers used by the game and display every frame

However, double buffering by itself does not eliminate screen tearing. Screen tearing still occurs if the display is drawing buffer X when the game wants to start writing to X. This usually happens only if the game is updating too quickly. The solution to this problem is to wait until the display finishes drawing its buffer before swapping. In other words, if the display is still drawing buffer X when the game wants to swap back to buffer X, the game must wait until the display finishes drawing buffer X. Developers call this approach **vertical synchronization**, or **vsync**, named after the signal that monitors send when they are about to refresh the screen.

With vertical synchronization, the game might have to occasionally wait for a fraction of a second for the display to be ready. This means that the game loop may not be able to achieve its target frame rate of 30 or 60 FPS exactly. Some players argue that this causes unacceptable stuttering of the frame rate. Thus, the decision on whether to enable vsync varies depending on the game or player. A good idea is to offer vsync as an option in the engine so that you can choose between occasional screen tearing or occasional stuttering.

Recent advances in display technology seek to solve this dilemma with an adaptive refresh rate that varies based on the game. With this approach, rather than the display notifying the game when it refreshes, the game tells the display when to refresh. This way, the game and display are in sync. This provides the best of both worlds as it eliminates both screen tearing and frame rate stuttering. Unfortunately, at this writing, adaptive refresh technology is currently available only on certain high-end computer monitors.

## Implementing Basic 2D Graphics

SDL has a simple set of functions for drawing 2D graphics. Because the focus of this chapter is 2D, you can stick with these functions. Starting in Chapter 5, “OpenGL,” you’ll switch to the OpenGL library for graphics, as it supports both 2D and 3D.

### Initialization and Shutdown

To use SDL's graphics code, you need to construct an SDL_Renderer via the SDL_CreateRenderer function. The term renderer generically refers to any system that draws graphics, whether 2D or 3D. Because you need to reference this SDL_Renderer object every time you draw something, first add an mRenderer member variable to Game:

```
SDL_Renderer* mRenderer;
```

Next, in Game::Initialize, after creating the window, create the renderer:

Click here to view code image

```
mRenderer = SDL_CreateRenderer(
    mWindow, // Window to create renderer for
    -1,      // Usually -1
    SDL_RENDERER_ACCELERATED | SDL_RENDERER_PRESENTVSYNC
);
```

The first parameter to SDL_CreateRenderer is the pointer to the window (which you saved in mWindow). The second parameter specifies which graphics driver to use; this might be relevant if the game has multiple windows. But with only a single window, the default is -1, which means to let SDL decide. As with the other SDL creation functions, the last parameter is for initialization flags. Here, you choose to use an accelerated renderer (meaning it takes advantage of graphics hardware) and enable vertical synchronization. These two flags are the only flags of note for SDL_CreateRenderer.

As with SDL_CreateWindow, the SDL_CreateRenderer function returns a nullptr if it fails to initialize the renderer. As with initializing SDL, Game :: Initialize returns false if the renderer fails to initialize.

To shut down the renderer, simply add a call to SDL_DestroyRenderer in Game :: Shutdown:

```
SDL_DestroyRenderer(mRenderer);
```

### Basic Drawing Setup

At a high level, drawing in any graphics library for games usually involves the following steps:

- 1. Clear the back buffer to a color (the game's current buffer).
- 2. Draw the entire game scene.
- 3. Swap the front buffer and back buffer.

First, let's worry about the first and third steps. Because graphics are an output, it makes sense to put graphics drawing code in Game :: GenerateOutput.
