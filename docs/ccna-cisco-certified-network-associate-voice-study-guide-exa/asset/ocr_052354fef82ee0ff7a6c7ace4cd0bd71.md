+   6. ☑ **A is correct.** The dspfarm profile 5 transcode command is correct. The correct sequence in the command is `dspfarm profile` followed by the profile ID and then the profile type, which can be conference, mp, or transcode.
+   
+   ☒ **B, C, and D are incorrect.** The command `dspfarm profile transcode 5` has the profile ID and the profile type in the wrong order. The `create dspfarm` command does not exist in Cisco IOS.

+   7. ☑ **A is correct.** The `maximum sessions 5` command is correct. This command should be entered in dspfarm-profile configuration mode.
+   
+   ☒ **B, C, and D are incorrect.** The commands `session 5`, `max-sessions 5`, and `maximum dsp actions 5` are not valid IOS commands.

+   8. ☑ **D is correct.** The flex mode allows for both medium and high complexity codecs, so the command `codec complexity flex` is correct.
+   
+   ☒ **A, B, and D are incorrect.** These three commands are simply invalid. The `codec complexity flex` command should be used instead.

+   9. ☑ **A is correct.** The `dsp services dspfarm` command assigns or allocates the DSP resources to a DSP farm. The command should be entered in voicecard configuration mode.
+   
+   ☒ **B, C, and D are incorrect.** These three commands are invalid.

+   10. ☑ **A is correct.** If the voice card is voice card 1, the proper command is `voice-card 1`. The command is always `voice-card` followed by the card number. This brief command places the router into voicecard configuration mode for the specified voice card.
+   
+   ☒ **B, C, and D are incorrect.** These three commands are invalid.

# LAB ANSWER

The three basic steps for configuring DSP farms are to configure the codec complexity, assign the DSP resources to a DSP farm, and configure a DSP farm profile. For example, to use DSP resources for transcoding, the commands in Figure 11-5 should be used.

Now that the DSP resources are configured, you can use the `show voice dsp` command to view information about the DSP resources, as shown in Figure 11-6 with the detail option used.

You can also use the `show running-config` command to view the DSP profile with the configuration as shown in Figure 11-7.