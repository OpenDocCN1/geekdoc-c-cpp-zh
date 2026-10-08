through one

```
// do polyphonic aftertouch stuff
break;
```

```
}
```

```
(float*) = cast the resulting pointer as float since we are 32-bit processing
data.outputs[0] = output bus 0
channelBuffers.32[i] = a pointer to the ith channel buffer
```

```
// data.outputs[0] = BUS 0
// note cast to float*, if 64-bit you cast to double
buffers[i] = (float*)data.outputs[0].channelBuffers32[i];
// sizeof us float, change to double for 64-bit version
memset(buffers[i], 0, data.numSamples*sizeof(float));
```

```
}
```

processing loop to watch the counters update. The loop

```
numSamples = samples left to process, used in while() loop
```

```
while(numSamples > 0)
{
t// do processing here
}
```

```
samplesProcessed = count of samples we've rendered
samplesToProcess = number of samples remaining
```

counters are highlighted along the snippet code. Here you can also see the code that uses the MIDI event's sampleOffset value to move the event into the next sub-block if needed. This ensures that MIDI events line up time with the rendered output.

```
result PLUGIN_API Processor::process(ProcessData&
data)
{}
```

First, you call the control update function to process the control changes that occurred during the block; we only process the last control event in the queue. If you want to process control events in a sample-accurate way, you need move this function into the processing loop and alter the function itself to extract control change points that line up with the block's sample offsets.