It's actually pretty easy to modify this module to work as an internal module for a plug-in. We need to provide a variable for the feedback sample and allow the user to set this value. We also need to provide a way to allow the user to get the current feedback value. Finally, we need a switch to allow the user to select the external feedback mode. That switch will be in the form of a boolean flag. After we get the variables set up, we can modify the processAudioFrame() function to use the external feedback sample.

# 7.4.1 DDLModule.h File

Declare the following new variables:

```
bool m_bUseExternalFeedback; // flag for enabling/disabling
float m_fFeedbackIn; // the user supplied feedback sample value
```

Also, declare and implement the get/set functions. They are so short you can just put them in the .h file rather than implementing them in the .cpp file.

```
// Add your code here: ------------------------------------------------------ //
float m_fDelayInSamples;
float m_feedback;
float m_fWetLevel;
void cookVariables();
void resetDelayline();
float* m_pBuffer;
int m_nReadIndex;
int m_nWriteIndex;
int m_nBufferSize;
bool m_bUseExternalFeedback; // flag for enabling/disabling
float m_fFeedbackIn; // the user supplied feedback sample value
// current FB is fb*output
float getCurrentFeedbackOutput()(return m_feedback*m_pBuffer[m_nReadIndex];)
// set the feedback sample
void setCurrentFeedbackInput(float f)(m_fFeedbackIn = f;)
// enable/disable external FB source
void setUseExternalFeedback(bool b)(m_bUseExternalFeedback = false;)
// END OF USER CODE ------------------------------------------------------ //
```

The current feedback sample output is found at m_pBuffer[m_nReadIndex] and multiplied by the feedback coefficient as per the block diagram. By allowing the user to get and set the feedback, we allow them to break into the loop and insert other effects, or use the feedback output for some other purpose altogether.

# 7.4.2 DDLModule.cpp File

processAudioFrame()

+   Modify the function to allow the use of externally supplied feedback samples: