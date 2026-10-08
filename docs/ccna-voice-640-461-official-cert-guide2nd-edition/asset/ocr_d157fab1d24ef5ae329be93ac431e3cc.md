transfer, conference, and so on) are still managed using SCCP or SIP, so those would not be available until the CME router came back online. Likewise, after the users disconnect from the call, the phone would not be available to place or receive any calls until the CME router returned online.

**Note:** This discussion assumes a CME deployment where there is no backup call-man-agement device. This is common for smaller organizations.

Let's broaden the discussion by following a call from a Cisco IP Phone to an analog phone attached to the PSTN shown in Figure 2-2.

**Figure 2-2** CME Call Flow for Calls to the PSTN

As the user of the Cisco IP Phone picks up the phone to place the call, all the communication- is handled by SCCP or SIP. After the user finishes dialing the phone number of the PSTN phone, the CME router realizes (due to its dial-plan) that the call needs to exit out PSTN-connected interface. CME now assumes the role of voice gateway and signals to the PSTN to establish the call on behalf of the Cisco IP Phone. Keep in mind that this is the "old school" signaling discussed in Chapter 1 when the CME router is attached to the PSTN using a digital (T1/EI) or analog (FXO) trunk. The audio for the call connects, the CME router assumes the role of converting between VoIP audio and PSTN audio. Because this connection is processor intensive, the CME router is equipped with Digital Signal-Processors (DSP), which are simply additional "mini processors" dedicated to voice functions.