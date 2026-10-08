```
--- check for control changes and update synth if
needed
doControlUpdate(data);

// --- we process 32 samples at
time
```

```
const int32 kBlockSize =
SYNTH_PROC_BLOCKSIZE;
```

Next, the audio buffers and clear them, storing each pointer in the buffers.

This code
initializes
t counter
and total
number of
samples for
t process
loop.

```
// initialize audio output buffers
float* buffers[OUTPUT_CHANNELS];
```

```
// clear the buffers 32-bit is float
for(int i = 0; i < OUTPUT_CHANNELS; i++)
```

```
{
    // data.outputs[0] = BUS 0
    buffers[i] = (float*)data.outputs[0].channelBuffers32[i];
    memset(buffers[i], 0, data.numSamples * sizeof(float));
```

This code
deals with
t MIDI
events that
arrived in
the

```
// --- total number of samples in the input Buffer
int32 numSamples = data.numSamples;
```

```
// --- this is used when we need to shove an event into the // next block
int32 samplesProcessed = 0;
```

data.inputEvents interface. Before entering the main processing loop, you setup an Event pointer and initialize it with
t first event.

The main while()
loop processes
both MIDI events
(first) then audio
rendering.
need to keep this
order so that we
pick up note on
and note
offreients before calling the voice object's rendering function.

```
// --- get our list of events
EventList* inputEvents = data.inputEvents;
Event e = [0];
Event* eventPtr = 0;
int32 eventIndex = 0;
```

This is the main audio rendering loop. You accumulate voices and write them out to the output buffers and set the
Samples for the next trip through the main loop. We will discuss the details of the rendering in depth 5
Chapters 5–13.