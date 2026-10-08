+   - follow the algorithms in the chapter, and if there is a quad phase variable, calculate this secondary output as

+   - sine uses a parabolic approximation
- saw (up and down) are extracted directly from modulo counter
- triangle and square are mathematically calculated via modulo counter
- exponentials uses the built-in convexInvertedFunction()
- the noise oscillators call a function in synthfunctions.h and then perform the hold using a counter to count sample periods of hold time

# LFO.h

```
class CLFO : public COscillator {
public:
    CLFO(void);
    CLFO(void);
```

```
// virtual overrides
void reset();
virtual void startOscillator();
virtual double doOscillate();
virtual void stopOscillator();
```

+   - for ramp and triangle, check the LFO mode and make unipolar for one-shot

+   - increment the modulo and return the amplitude-scaled output

+   - calculate normal and quad phase outputs by multiplying the output and amp modulation values

#  5.32 The CQBLimitedOscillator Object

Add new class to your project named CQBLimitedOscillator and make sure to set its base class to Oscillator. Refer to the code listing below and copy it into your file (or, alternatively you can download the sample code). Figure 5.47 shows the class diagram for CQBLimitedOscillator.

```
CLFO::CLFO(void) {
    m_uLFOMode = sync;
}
```

```
void CLFO::reset() {
    // --- call base class
    COscillator::reset();
}
```

# CQBLimitedOscillator Member Variables

There are no extra members to declare; they are all in the base class.

# CQBLimitedOscillator Member Methods

Aside from the class overrides (reset), startOscillator() and stopOscillator() are sub-functions to handle each of the three oscillator types. The function doOscillate() will call these sub-functions for sawtooth, square and triangle waveforms and directly calculate the other noise waveforms.

# Constructor

+   - there is nothing to do here because it is all done in the base class

# reset ()

+   - always call the base class method first
- adjust the starting phase of the modulo counter for sawtooth and triangle waves

Figure 5.47: Class diagram for the CQBLimitedOscillator object.

# startOscillator ()

+   - call reset()
- set the one note on flag

# stopOscillator ()