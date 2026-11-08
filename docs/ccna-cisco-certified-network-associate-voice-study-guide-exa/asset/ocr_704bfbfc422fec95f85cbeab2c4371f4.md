is based on the perception of the hearer and is impacted by that hearer’s experience. For example, if the hearer has been exposed to very high quality audio communications, he or she will be more likely to notice poor voice quality on a VoIP conversation. By the same token, a person who has not been exposed to such quality is less likely to perceive the same voice signal as being poor. This reality is not unlike the experience we’ve had with high speed Internet. I have very fast Internet throughput at my home. I consider it high speed. When I go to a hotel with less than 1/10 the throughput, I don’t consider that high speed even though the hotel does. A fast Internet connection to one is a slow connection to another.

Even with this subjectivity, an industry standard for judging voice quality has been developed. This standard is known as the Mean Opinion Score (MOS). The MOS is based on responses from a group of participants, and it attempts to remove some of the subjectivity through the process of averaging the participants’ responses.

Factors that impact voice quality include clarity, delay, and echo. Clarity is a perceptual measurement of an original sound compared with a digitized signal. Delay causes the perception of a continuous voice signal (like the continuous sound waves in a face-to-face communication) to be lost. Echo causes the voice signal to be reflected back toward the speaker. This echo can result in overlapping sounds and can reduce quality.

# Clipping

Clipping occurs when parts of the sound waves are lost during digital communications. This can occur as a result of many different problems:

+   - Processing overload on the encoder due to insufficient hardware
+   - Dropped packets between the sender and receiver due to media errors or other problems
+   - Overflows or underflows on the jitter buffer
+   - Network latency causing too much delay and forcing dropped packets
+   - Using a half-duplex speakerphone

When full-duplex speakerphones are used, they usually sample the environment to build a digital image of the noise floor within the area. This image is used to distinguish between a human speaker and the background noise. Half-duplex speakerphones do not do this and may interpret the background noise as a human speaking, which may in turn result in clipping.

Whatever the cause, remember that clipping is the loss of portions of sound within the digital stream of communications.