# 8.5.2.3 Synchronization Issues

For the above described scheme to work, the receiver and the transmitter must remain synchronized for the duration of the transmission. This synchronization can be achieved by one of the techniques described in Section 8.3.4.2.

```
1:  procedure CNSTRANSMIT(IN bit vector *data_frame*, IN integer *frame_len*)
2:      **var** *trans_len* : **Integer**;                    ▷ *trans_len* is half of binary frame length
3:      *trans_len* = \frac{*frame_len*}{2};
4:      **Transmit** *trans_len*;                              ▷ length of CNS data
5:      Determine the *BpSMapping* using either *Scheme 1* or *Scheme 2*; ▷ bit pair to symbol mapping
6:      **Transmit** *BpSMapping*;                             ▷ obtained using either Scheme 1 or 2
7:      **for** *i* = 0 to *frame_len* step 2 **do**
8:          Determine symbol *sym* to be transmitted based on
9:          *BpS Mapping* of bits *data_frame[i]* and *data_frame[i + 1]*;
10:         **Transmit** symbol *sym*;                          ▷ either A, B, C or N
11:     **end for**
12: **end procedure**
```

```
1:  procedure CNSRECEIVE(OUT bit vector *recv_data*)
2:      /* *time_slot[i]* refers to the *i*th time slot */
3:      **var** *j* : **Integer**;                             ▷ counter for output buffer *recv_data*
4:      *j* ← 0;
5:      **Receive** *trans_len* from transmitter;              ▷ length of the transmitted CNS data
6:      **Receive** *BpSMapping*;                              ▷ transmitter first sends the BpS Mapping
7:      **for** *i* = 0 to *trans_len* **do**
```