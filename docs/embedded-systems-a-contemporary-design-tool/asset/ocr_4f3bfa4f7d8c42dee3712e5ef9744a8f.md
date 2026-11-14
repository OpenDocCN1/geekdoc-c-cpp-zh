![](bbox=[0.28, 0.06, 0.76, 0.21])

# Figure 16.34 Clock Encoding Using Bipolar Encoding

Observe in the diagram in Figure 16.34 that the signal returns to zero level after each encoded bit. Such a scheme is referred to as return-to-zero (RZ) signaling. The approach requires three distinct signal levels.

# return-to-zero (RZ)

# MANCHESTER PHASE ENCODING

# Manchester Phase Encoding

Manchester Phase Encoding In a Manchester Phase Encoding scheme, a binary 0 is encoded as a high to low signal transition and a binary 1 as a low to high signal transition. The transition occurs in the center of each bit cell, which provides the clock information.

Observe in Figure 16.35 that the signal does not return to zero level after each encoded bit. Such a scheme is referred to as a nonreturn-to-zero (NRZ) signaling.

# nonreturn-to-zero (NRZ)

![](bbox=[0.28, 0.45, 0.76, 0.57])

# Figure 16.35 Clock Encoding Using Manchester NRZ Phase Encoding

# MANCHESTER DIFFERENTIAL ENCODING

# Manchester Differential Encoding center start

With Manchester Differential Encoding, illustrated in Figure 16.36, once again the transition occurs in the center of each bit cell and provides the clock information. We have a transition at the start of each bit cell only if the next bit to be encoded is a binary 0.

![](bbox=[0.28, 0.72, 0.76, 0.84])

# Figure 16.36 Clock Encoding Using Manchester NRZI Differential Encoding