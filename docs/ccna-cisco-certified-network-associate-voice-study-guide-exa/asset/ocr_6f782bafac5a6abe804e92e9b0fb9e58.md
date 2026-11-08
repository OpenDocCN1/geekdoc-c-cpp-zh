# # TWO-MINUTE DRILL

# ## 640-460: Describe the Process of Voice Packetization

+   - Sampling is the process used to gather numeric data that represents the electrical signals received from a microphone.
+   - The Nyquist theorem specifies that twice the number of samples must be taken as the highest frequency in the sound.
+   - Most human speech comprises frequencies up to 4,000 Hz or 4 KHz. For this reason, 8,000 samples per second work well for human speech sampling.
+   - Quantization is the process used to assign the samples to codes representing the audio information in the samples.

# ## 642-436: Describe Codecs and Codec Complexity

+   - A codec is used to encode and decode audio information for storage or transmission.
+   - Codec complexity is a reference to the processing power required to perform the operations demanded by a codec.
+   - More complex processes such as compression and error corrections increase codec complexity.
+   - Increased codec complexity demands increased DSP resources, but reduces network bandwidth consumption.
+   - The Cisco IOS codec complexity command is used to set the complexity level.
+   - The codec complexity command can be used to set the complexity level to high, medium, flex, and secure.

# ## 640-460: Describe the Function of and Differences between Codecs

+   - The G.711 codec operates at 64 kbps, and the G.729 codec operates at 8 kbps.
+   - The G.711 codec does not use compression and is a medium complexity codec in Cisco hardware.
+   - The Mean Opinion Score (MOS) is a common rating used to measure the quality of codecs.