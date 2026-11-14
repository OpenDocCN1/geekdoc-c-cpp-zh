The block diagram in Figure 16.33 illustrates the design.

![](bbox=[0.265, 0.11, 0.905, 0.26])

# Figure 16.33 A High-Level Block Diagram for a System Utilizing Bit Sampling at the Receiver

# 16.6.1.5 Analysis

The potential problems with an asynchronous approach include the following:

+   - It is difficult to test.
+   - Clock noise is more difficult to filter out.
+   - The protocol to identify the start/end of transmission is potentially a bit more complex than a synchronous scheme.

At the same time, the asynchronous approach can offer several advantages.

+   - The devices within the system can run at different/differing speed.
+   - There will be no clock skew on long busses.

# 16.6.2 Synchronous Information Exchange

The asynchronous transmission schemes have several drawbacks, including the extra overhead of control bits and the bit clock synchronization scheme, which becomes less reliable at higher data rates. Such problems can be mitigated to a large extent with synchronous transmission. Nonetheless, it is still necessary to achieve bit, character, and frame synchronization. Frame synchronization is usually derived from bit or character synchronization. With synchronous transmission, exchanges between the sender and receiver are synchronized to the clock either directly or through signals encoded in the data.

# 16.6.2.1 Bit Synchronization

To achieve bit synchronization, a two-step process is typically used:

+   - Encode the clock in the data.
+   - Re-derive the clock from the data.

# 16.6.2.1.1 ENCODED CLOCK

To encode the clock in the data, three different methods or their variants are commonly used.

# BIPOLAR ENCODING

When using bipolar encoding, binary 0’s and 1’s are represented by different polarity signals, as is shown in Figure 16.34. Each bit cell contains clocking information, as reflected by the transition in the center of the bit cell.