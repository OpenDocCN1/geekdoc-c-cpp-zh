```
bool __stdcall CDynamicsProcessor::processAudioFrame(float* pinpBuffer, float*
 poutputBuffer,
 UINT uNumInputChannels,
 UINT uNumOutputChannels)
{
 // calculate gains
 float fInputGain = pow(10.0, m_fInputGain_dB/20.0);
 float fOutputGain = pow(10.0, m_fOutputGain_dB/20.0);

 // setup stereo link
 float xn_L = fInputGain*pInputBuffer[0];
 float xn_R = 0.0; // for later

 // do Left
 float fLeftDetector = m_LeftDetector.detect(xn_L);
 float fRightDetector = fLeftDetector; // use in case of mono file

 // check for right side; can use again in right side code
 if(uNumOutputChannels == 2)
 {
 // get the right side
 xn_R = fInputGain*pInputBuffer[1];

 // detect it
 fRightDetector = m_RightDetector.detect(xn_R);
 }

 // start with Left
 float fLinkDetector = fLeftDetector;
 float fGn = 1.0;

 if(m_uStereoLink == ON) // this works even with mono files
 {

 // detectors output log values; convert to linear to sum them
 fLinkDetector = 0.5*(pow(10.0, fLeftDetector/20.0) + pow(10.0,
 fRightDetector/20.0));

 // convert back to log
 fLinkDetector = 20.0*log10(fLinkDetector);
 }
 // branch
 if(m_uProcessorType == COMP)
 fGn = calcCompressorGain(fLinkDetector, m_fThreshold, m_fRatio,
 m_fKneeWidth, false);
 else if(m_uProcessorType == LIMIT)
 fGn = calcCompressorGain(fLinkDetector, m_fThreshold, m_fRatio,
 m_fKneeWidth, true);

 etc... same for other branches

 // delay the left DCA
 float fLookAheadOut = 0;
 m_LeftDelay.processAudio(&pInputBuffer[0], &fLookAheadOut);

 <SNIP SNIP SNIP>
```