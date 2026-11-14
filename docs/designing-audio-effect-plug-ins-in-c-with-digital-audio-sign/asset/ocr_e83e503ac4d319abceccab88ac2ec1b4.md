```
// invert output
bool m_binvert;

// Reset the read index
void reset()
{
    m_fReadIndex = 0.0;        // top of buffer
    m_fQuadPhaseReadIndex = 256.0; // 1/4 of our 1024 point buffer
}
```

# 9.8.2 WTOscillator.cpp File

# Constructor

+   Initialize the new index variable in the constructor; it will be reset to the proper value later.

```
CWTOscillator::CWTOscillator()
{
    <SNIP SNIP SNIP>
    // clear variables
    m_fReadIndex = 0.0;
    m_fQuadPhaseReadIndex = 0.0;
    m_f_inc = 0.0;

    // silent
    m_bNoteOn = false;

    // norm phase
    m_binvert = false;
    etc...
}
```

# 9.8.3 WTOscillator.h File

Add the doOscillate() function. It needs to be called externally in future projects. It also needs to provide both quad phase outputs. It will be a mono function. It requires no input argument and we can test it from within the plug-in by sending the two phases out to the left and right channels, then view it with the analyzer. In the .h file, add the following:

```
// Add your code here: ---------------------------------------//
// function to do the Oscillator; may be called by an external parent Plug-In too
// pYn is the normal output
// pYqn is the quad phase output
void doOscillate(float* pYn, float* pYqn);

// Array for the Table
float m_SinArray[1024];        // 1024 Point Sinusoid
float m_SawtoothArray[1024];   // saw
float m_TriangleArray[1024];   // tri
float m_SquareArray[1024];     // sqr

Etc...
```

# 9.8.4 WTOscillator.cpp File

Add the new function doOscillate() to the .cpp file. Cut and paste the contents of the