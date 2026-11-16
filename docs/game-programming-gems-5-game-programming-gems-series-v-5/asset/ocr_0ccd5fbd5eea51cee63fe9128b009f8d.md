![](bbox=[0.196, 0.085, 0.86, 0.255])

# FIGURE 7.5.1 Speech production model.

Our languages use two different types of sound: the voiced sound, produced by the vibration of the vocal cords (for example, vowels); and the unvoiced sound, which does not use the vocal cords (such as consonants t, v, and s). Figure 7.5.2 shows a comparison between voiced and unvoiced sounds. The phoneme u is a voiced sound, whereas s is an unvoiced sound.

![](bbox=[0.2, 0.495, 0.94, 0.6])

# FIGURE 7.5.2 Comparison between (a) voiced sound and (b) unvoiced sound.

The major problem when dealing with speech is the great instability of the produced signal. Actually the production of speech is dependent on the brain's control of different organs: the lungs, the vocal cords, the tongue, and others. As our ear is insensitive to these weak variations, these are not controlled consciously. For a computer system, it is necessary to extract features as independently as possible from these variations.

An important parameter of a speech signal is its fundamental frequency, also called pitch. The fundamental frequency of a speech signal is the frequency at which the vocal cords vibrate. For a man, it varies from 70 to 250 Hz, while for a woman or a child, it varies from 200 to 600 Hz. Due to the high variability of the pitch, features independent from it need to be extracted.