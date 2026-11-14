| CWaveTable | |
| Member Variables | Purpose |
| --- | --- |
| float m_SinArray[1024]; float m_SawtoothArray[1024]; float m_TriangleArray[1024]; float m_SquareArray[1024]; | Arrays to store the non-band limited wave tables |
| float m_SawtoothArray_BL5[1024]; float m_TriangleArray_BL5[1024]; float m_SquareArray_BL5[1024]; | Arrays to hold the band-limited wave tables |
| float m_fReadIndex; float m_fQuadPhaseReadIndex; | Indices for reading the wave table |
| float m_f_inc; | Table increment value for current output frequency |
| int m_nSampleRate; | Sample rate IMPORTANT: Needed for calculation of table inc; do not forget it! |
| float m_fFrequency_Hz; | Oscillator frequency |
| bool m_bInvert; | Flag to invert output |
| UINT m_uOscType; enum{sine, saw, tri, square}; | Enumerated unsigned integer type (UINT) for osc waveform type |
| UINT m_uTableMode; enum{normal, bandlimit}; | Enumerated UINT for table mode (we will use normal mode in this plug-in since the oscillator is a LFO) |
| UINT m_uPolarity; enum{bipolar, unipolar}; | Enumerated UINT for osc polarity (we will use unipolar for this plug-in) |
| Member Functions | |
| void doOscillate(float* pYn, float* pYqn) Parameters: • float* pYn • float* pYqn | The oscillate function Output: pYn is the normal output Output: pYqn is the quadrature phase output |
| bool prepareForPlay() | The prepareForPlay() function for the oscillator; same use as a |