+   - inChannel: MIDI receive Channel
- inPitch1 and inPitch2: the LSB and MSB of the pitch bend message

First convert the LSB and MSB into a 14-bit word and decode.

The Control Change Messages are handled in HandleControlChange() with the arguments:

+   - inChannel: the MIDI channel
- inController: the MIDI CC index
- inValue: the CC value 0 to 127

All synths respond to a default set of CCs:

+   - Mod Wheel
- Volume CC7
- Pan CC10
- Expression CC11