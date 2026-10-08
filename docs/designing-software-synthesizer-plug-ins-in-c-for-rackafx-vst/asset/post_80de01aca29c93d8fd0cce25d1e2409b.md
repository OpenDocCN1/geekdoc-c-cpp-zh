
in reverse. This is shown in Figure 13.2, where we are using a pointer and index offset to access a circular buffer. The index offset is +5, so the pointer moves in steps of five buffer locations, skipping through. When it skips the end boundary, it wraps back to the top and offsets the same number of buffer locations.

Suppose we have using the pointer to write audio samples into this buffer and that has been going for some time that the pointer has wrapped around the top a few times. If we freeze during a write-event and think about the contents of the buffer, we can see how the samples line up in time. Let's assume we are using an index value $m_{nwrite}$ to keep track of the write location in the buffer, incrementing it by each sample period. We are going to use another index $m_{nread}$ to read values from the array. In Figure 13.3(a) you can see that the oldest sample in the buffer is the one we are writing. The youngest sample is one location before the write location. The other values are between the oldest and youngest. If we want to delay the signal by 100 samples, we offset the read index 100 samples before the write index; this might mean that the index wrap around the top of the buffer. As Figure 13.3(b) shows, the difference between the read and write index determines the delay time.

So, by implementing a circular buffer and reading/writing audio samples from/to, we can create a basic delay. This delay time is set in samples, not seconds or milliseconds. And as it turns out, we need more precision than the sample period has to offer. For example,

![](img/b42d0dca53f4a889d8162d55f7c8c05d_867_0.png)

Figure 13.1: MiniSynth with an effects upgrade adds an insert effect (compressor) and master effect (delay)—notice that the delay effect allows you to modulate some of its parameters with MIDI; in this chapter we will design the delay effect, while the FX modulation is left as a Chapter Challenge.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_867_1.png)

Figure 13.2: The circular buffer access operation: as the pointer moves across the end boundary, it wraps back to the top.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_868_0.png)

Figure 13.3: (a) The oldest delay in the buffer is the one we are to write over. (b) The offset between the read and write pointers determines the delay time in samples.

at 44.1 kHz, the sample period is 23µs. That might seem like a small value, but if that is the resolution of our delay effect, we will have problems if the user tries to synchronize the delay time to the beats per minute (BPM) of the song. If the delays do not fall precisely on the required intervals, the delay will drift over time. It might take a while, but during a long song, the delay could drift significantly. Therefore we need to be specify and implement—a fractional delay time with the delay value in milliseconds. This means we need to be able to read out values that are between two actual values; the delay is a fraction of the distance of one sample. A simple way to do this is with interpolation. Interpolators are inherently low filters, the convenience and ease of implementation makes them attractive. See the Bibliography for more information on fractional delays and with filtering.

Since linear interpolation is the simplest form, let's look at that operation. There are several ways to implement interpolation, treat it like a DSP filter rather than y = mx + b. You can also view interpolation as a weighted sum operation. For example, if the interpolation point is 0.5 between samples 1 and 2, then the interpolated value is made up of 50% of sample 1 plus 50% of sample 2. Suppose we want a fractional delay of 23.7186 samples. The interpolated distance is 0.7183 between samples 23 and 24. We can call the fractional component `frac` and the integer part `int`. The scheme is shown in Figure 13.4. We can re-map the samples 23 and 24 to index values 0 and 1, then interpolate the frac distance between them. We can then write the interpolated output as:

```
interp_output = frac * (Sample 24) + (1-frac) * (Sample 23)
interp_output = 0.7183 * (Sample 24) + 0.2817 * (Sample 23)
```

Here is a linear interpolation function you can use; it is already declared in `constants.h`:

```c
float dLinp(float x1, float x2, float y1, float y2, float x);
```

You give it a pair of data points (x1, y1) and (x2, y2) plus a distance between them on the x-axis (x) and it returns the interpolated value using the weighted sum method. Interestingly, this interpolator can be viewed as a filter—a first order feed-forward as shown in Figure 13.5.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_869_0.png)

**Figure 13.4:** (a) A fractional delay of 23.7183 is desired and can be seen as (b) a weighted sum of the two known values using (1-frac) and (frac) and operating on a sub-sample basis, allowing us to re-index the x-axis and frac.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_869_1.png)

**Figure 13.5:** A linear interpolator viewed as a feed-forward filter.

## Delay Effect Topology

Our delay effect includes two structures, for the left and one for the right. These are basic delay lines with feedback. A single delay line with feedback is shown in Figure 13.6. The delay implements $z^{-D}$ or $D$ samples of delay, and it is a circular buffer. Notice that the value into the delay line is a sum of the input $x(n)$ and the current output $y(n)$, scaled by a feedback value. This leads to the “read before write” paradigm which we use on all delay effects. It means that we read the feedback value first, then the input into the delay line. The user can adjust the delay from zero to some maximum (D seconds). When the user changes the delay line, they are really changing the distance between the read and write index values. In our plugin, the delay object will handle this wet/dry mixing.

In order for the delay to be interesting, we need to add the dry unprocessed signal to the delayed output. In our systems, the wet/dry mix is part of the main plugin. Our delay object is fully self-contained. Figure 13.7 shows the basic stereo delay with feedback and wet/dry components.

We can spin off variations on the basic delay, giving our delay effect four different algorithms. The first is the stereo delay. We allow the user to adjust the delay between left and right as a ratio. The second is the ping-pong delay shown in Figure 13.8. The ping-pong delay crosses both the input and feedback paths to the opposite channel. It produces a circular kind of delay sound that starts in the center multi-tap delay.

A multi-tap delay has multiple outputs from the delay line. Ours have two taps—the main delayed output and a second delay with a shorter value for each channel. This will produce two slightly different variations, as shown in Figure 13.9: in the tap1 version, the feedback is taken only from the main delay output. In tap2, the feedback is a mix of the normal and second tap outputs. You will notice a difference in sound between the two modes; tap1 will sound more rhythmic and less dense, tap2 is thicker and fuller. Also, both work well with short delay times, long feedback, and low ratio values—they will ping and ring at various frequencies as the delay times get short and they become more like filters than delays.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_870_0.png)

Figure 13.6: The basic delay with feedback structure.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_870_1.png)

Figure 13.7: The basic stereo delay with feedback and wet/dry mix controls.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_871_0.png)

Figure 13.8: The ping-pong delay crosses inputs and feedback for a recirculating effect.

In the multi-tap versions, we will not use two separate buffers for each channel; instead, we will use one buffer and read two index values—the normal output and a secondary output. The tap1 topology could be redrawn as in Figure 13.10, showing how one delay line produces both outputs. It also shows the nature of the delay control; for these two effects, the ratio controls the length of the secondary tap compared to the main tap.

## 13.3 The CDelayLine Object

The CDelayLine object handles the low operation of a single delay with no feedback and no wet/dry path. It is only the delay line core. You can use this object (or many of them) to create complex delay effects. We will use two of these objects as another C++ object called CStereoDelayFX, which you use as the basis for a large and robust set of delay effects if you are so inclined.

The variables consist of all the attributes of the single delay line. The read and write index values are crucial to operation.

Initialize the variables and reset. The destructor (not shown) will delete the buffer.
