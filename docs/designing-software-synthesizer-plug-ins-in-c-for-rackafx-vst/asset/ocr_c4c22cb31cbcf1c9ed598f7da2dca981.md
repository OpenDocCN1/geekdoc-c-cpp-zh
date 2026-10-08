together, however before writing to the outputs, we declare accumulator variables as well as the normal voice output variables. two oscillators are mixed with scalar values of 0.5 to try to minimize clipping. We will discuss the code that deals with stealing and turning off the oscillators in the next section so it for now.

# Processor::Processor()

```
// -- initialize mod ranges
nm_dOscFoModRange = OSC_FO_MOD_RANGE;
m_dFilterModRange = FILTER_FC_MOD_RANGE;
m_dOscFoPitchBendModRange = OSC_PITCHBEND_MOD_RANGE;
m_dAmpModRange = AMP_MOD_RANGE;
```

# 8.16 Dynamic Voice Allocation

Voice stealing (also called voice allocation or dynamic voice allocation) is a by-product of polyphony, and it can be tricky and complicated. If the user triggers a new note the supply of voices is exhausted, you need a shut one voice off and steal it for the new note. Deciding on which voice to terminate is up to you, the synth designer. A heuristic is used to decide on the fate of the stolen note. Heuristics trade-offs involve their mechanism; all have their strengths and weaknesses. Some options are:

+   - steal the oldest note
- steal the oldest note that isn't the lowest pitched note
- steal the note with the lowest velocity
- steal the first note that has already been released
- steal notes that are inside of chord voicings