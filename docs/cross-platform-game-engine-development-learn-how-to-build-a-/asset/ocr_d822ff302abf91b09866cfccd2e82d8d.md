The SDL_RenderClear() function will clear the renderer so that the next frame can be rendered into it. We also can change the background color, but we will talk about that later.

To initialize the SDL_mixer, we must call Mix_OpenAudio(). The first argument sets the frequency of the sound. 44100 is a common frequency supported by most systems. The second argument defines the sample format, which in this case is set to the default. The third argument is the number of hardware channels, which is two for stereo in this case. The fourth argument is the sample size, which defines the size of the chunks we use when playing sound. 512 is the value that fits for me if you ever have issues when playing song, try other values like: 1024 (1kb) or 2048 (2kb).

If you compile and run your code, a blank window will appear like below.

![](bbox=[0.08, 0.36, 0.9, 0.475])

Figure 20 First Window (Windows)

![](bbox=[0.08, 0.51, 0.9, 0.64])

Figure 21 First Window (Linux)

As you might have noticed, you can't really do much with these windows right now because they won't respond to any event. Let's create an event system to manage all events for us.