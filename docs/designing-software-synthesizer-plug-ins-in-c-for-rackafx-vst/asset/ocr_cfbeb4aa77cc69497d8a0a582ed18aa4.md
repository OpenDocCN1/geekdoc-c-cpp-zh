```
void CDDelayLine::resetDelay()
{
    // --- flush buffer
    if(m_pBuffer) {
        memset(m_pBuffer, 0, m_nBufferSize*sizeof(double));
    }

    // --- init read/write indices
    m_nWriteIndex = 0;
    m_nReadIndex = 0;

    // --- cook
    cookVariables();
}
```

# setSampleRate()

Set the sample rate variable. This is important since the object calculates delay time based upon it.

void setSampleRate(int nFs) (m_nSampleRate = nFs);

# setDelay_mSec()

Set the delay time in milliseconds, then cook the variables to convert the delay time into an offset between read and write index values.

# cookVariables()

Convert the delay time to an offset between read and write index values. Remember that the read index is behind the write index, so the index is subtracted. We need to check to see, however, if we have gone past the beginning of the array and wrap around to the other end if needed.

```
void CDDelayLine::setDelay_mSec(double dmSec)
{
    // --- save
    m_dDelay_ms = dmSec;

    // --- cook
    cookVariables();
}
```