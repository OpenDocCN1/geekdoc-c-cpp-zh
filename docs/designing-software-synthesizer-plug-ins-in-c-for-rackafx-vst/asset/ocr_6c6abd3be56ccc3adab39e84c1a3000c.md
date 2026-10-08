```
// --- get the matrix core
modMatrixRow** getModMatrixCore(){return m_ppMatrixCore;}

// --- set the matrix core
void setModMatrixCore(modMatrixRow** pModMatrix)
{
    if(m_ppMatrixCore)
    {
        for(int i=0; i<m_nSize; i++)
        {
            // delete pointer
            modMatrixRow* pRow = m_ppMatrixCore[i];
            delete pRow;
            m_nSize--;
        }
    }
    m_nSize = 0;
    delete [] m_ppMatrixCore;
}

m_ppMatrixCore = pModMatrix;
m_nSize = getMatrixSize();
```

clearSources() and clearDestinations()

This is followed with simple clearing methods for the source and destination arrays and the matrix core. The clearDestinations() function is called every time the modulation matrix runs since it accumulates values into the Destinations array.