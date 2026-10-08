optimization here involving the oscillators; if you hard code the oscillator members, you don't have to check their pointers, the object will not be as flexible.

```
void CVoice::reset()
```

Figure 9.8: The CVoice Note on logic.

```
{
    if(m_p0sc1)m_p0sc1->reset();
    if(m_p0sc2)m_p0sc2->reset();
    if(m_p0sc3)m_p0sc3->reset();
    if(m_p0sc4)m_p0sc4->reset();
```

# Off Logic

The note offlogic is much simpler than the note on logic. The flowchart is shown in Figure 9.9. The EGs can only be turned off:

+   - the note is ON and the output EGs are in a non-note off state
- the number is the same as the playing note

```
if(m_pFilter1)m_pFilter1->reset();
if(m_pFilter2)m_pFilter2->reset();
```

Figure 9.9: The CVoice note logic.

```
m_EG1.reset();
m_EG2.reset();
m_EG3.reset();
m_EG4.reset();
```

If the note off is for a note that is pending but not yet playing, just clear the pending flag and let the note continue.

# noteOff()

The noteOff() function follows the flowchart. Notice that the function canNoteOff() is used in the logic. The canNoteOff() is overridden when a synth voice uses other EG(s than the output EG. This happens in DXSynth. All other synths use the output EG (Note: if you use a different EG, you will need to modify the canNoteOff())

```
m_LF01.reset();
m_LF02.reset();
m_DCA.reset();
```

```
inline void initGlobalParameters(globalSynth* globalParams)
{
    // save Global Param Ptr
    m_pGlobalSynthParams = pGlobalParams;
```

function too.)

Figure 9.10: The CVoice doVoice() flowchart.

# doVoice() Logic

The CVoice class handles the low level rendering operations common to all synths. You will always override this in your derived synth voice objects, and you will always call this class function first; if it returns false, then there is no note to render, which can happen if the note has just ended. The flowchart for doVoice() function is shown in Figure 9.10. Note that it only returns true if a note is currently playing or we stole a voice.

Compare the code to the flowchart to make sure you understand the implementation. Notice the way the portamento works. If portamento is enabled when a note is transferred, the portamento start pitch is the current portamento pitch value. If the function makes to the marked Portamento Block, then a note is currently playing. It have just ended. The portamento event ends and the pitch has reached the target. If not, it calculates the new pitch for the current sample period. Your derived class will call this function first, add voice-specific