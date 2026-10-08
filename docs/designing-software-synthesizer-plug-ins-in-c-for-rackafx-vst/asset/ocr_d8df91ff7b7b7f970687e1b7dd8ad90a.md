Now that you've seen the CVice base class, the modulation matrix, and voice modes, let's look at the derived class inline virtual void noteOff(uMIDINoteNumber) for our

```
// --- no note on, ignore
if(m_bNoteOn && canNoteOff())
{
// --- if note pending is this note, clear flag
if(m_bNotePending && uMIDINoteNumber == m_uMIDINoteNumberPending)
{
    m_bNotePending = false;
    return;
}
// --- only shut off our note
if(uMIDINoteNumber != m_uMIDINoteNumber)
    return;
// --- else, do the note off event
m_EG1.noteOff();
m_EG2.noteOff();
m_EG3.noteOff();
m_EG4.noteOff();
}
```

MiniSynth Project. Hopefully you will be delighted with its simplicity; the base class handles most of the low level chores. Open MiniSynthVoice.h and .cpp, and we will go through the variables and functions. The oscillators and filter are declared first. Notice the enumeration for voice mode is repeated from the GUI for ease of coding.

# Constructor

The constructor performs the following initializations, some of which you may modify:

+   - connects oscillators to member pointers
- connects the filter to member pointer
- turns offNLP on filter (optional)
- sets the m_dAuxControl to the filter to 0.75 for passband compensation (more basic)
- initialize oscillators to voice mode 0 (optional)
- set EG mode to analog (optional)