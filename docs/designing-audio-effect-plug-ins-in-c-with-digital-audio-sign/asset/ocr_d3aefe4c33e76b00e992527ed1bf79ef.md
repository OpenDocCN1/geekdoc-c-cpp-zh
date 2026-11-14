# 10.1 The Flanger/Vibrato Effect

The flanger effect gets its name from the original analog method of running two tape machines slightly out of sync with each other by placing a thumb on the flange (the ring that holds the tape) of one machine's reel and applying pressure to slow down the tape ever so slightly. Other variations include rubbing the flange circularly. The effect creates a time-varying delay that falls out of sync, then back in sync with the first tape machine. The effect has been compared to the whoosh of a jet engine, or the sound of a phaser effect. No matter how you define it, the flanger has a unique sound. The effect is heard on numerous recordings.

In order to simulate the flanger effect, you need a delay line whose read index moves away from, then back to the top or starting point of the delay. When the read pointer is back to the top, there is no delay and as it moves away from the write index, the pitch is modulated down. When the index turns around and moves back, the pitch is modulated up—this is the Doppler effect in practice. When the output of the modulated delay is sent 100% wet, with no dry signal, the effect is that of vibrato—the pitch shifts up and down as the pointer moves back and forth. When the dry signal is mixed with the wet signal, the pitch shifting changes into the flanging effect. The amount of delay time varies between 0 and about 7–10 mSec; at a 44,100 Hz sample rate, this corresponds to around 308 to 410 samples. Feedback is usually added to increase the effect by creating resonances or anti-resonances, depending on whether the feedback is normal or inverted.

Figure 10.2 shows the two states of the modulator with increasing and decreasing pitch shifting due to the Doppler effect. Figure 10.3 shows alternate ways of diagramming the same modulator. The vibrato and flanger are the same effect underneath the hood—it’s only the mix ratio that determines which effect you have. Because the delay is constantly moving around we are once again faced with options on how to handle the fractional delay that is required; after you calculate the number of samples of delay (which will most likely have a fractional component) you can

+   - Truncate the value and just use the integer part.
+   - Round the value up or down.

![](bbox=[0.22, 0.65, 0.82, 0.9])

Figure 10.2: (a) As the delay increases, the pitch drops. At the end of the delay, the index turns around and begins heading back toward the write index (b), increasing the pitch; the maximum delay here is about 10 mSec at 44,100 Hz.