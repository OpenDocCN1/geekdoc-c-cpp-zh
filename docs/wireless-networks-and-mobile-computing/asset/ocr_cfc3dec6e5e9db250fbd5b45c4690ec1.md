The transmission protocol of TSS thus consists of two steps:

# Protocol TransmitTSS

**Step 1:** Recode the binary data to ternary using the *Binary2Ternary* protocol.

**Step 2:** Transmit the ternary data symbol by symbol, obtained by the recoding process from step 1 using the following rules:

**Step 2.1:** If the symbol to be transmitted is 0, then switch off the transmitter for the symbol period.

**Step 2.2:** Otherwise, switch on the transmitter and transmit the symbol (1 or 2) in the time slot.

The receiver side protocol would be the reverse of that for the transmitter:

# Protocol ReceiveTSS

**Step 1:** Receive the ternary encoded data symbol by symbol as follows:

**Step 1.1:** If a signal is received in the given time slot (symbol period), the received symbol is either a 1 or a 2, depending on the predetermined received signal-to-symbol mapping.

**Step 1.2:** Otherwise, if the channel is quiet, the received symbol is a 0.

**Step 2:** Convert the received ternary message to binary using the *Ternary2Binary* protocol.

# 8.4.2  Performance Analysis

The TSS transmission scheme involves the recoding of an outgoing binary message to its equivalent ternary form and transmitting it. The receiver then reconverts