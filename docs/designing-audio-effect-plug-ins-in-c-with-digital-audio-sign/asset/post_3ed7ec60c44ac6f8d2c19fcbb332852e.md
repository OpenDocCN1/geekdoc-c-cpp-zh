
![](img/b54974d0a4317ec82d7ae02126d10a6f_337_0.png)

Figure 10.15: DPS M7 multi-flanger.

![](img/b54974d0a4317ec82d7ae02126d10a6f_337_1.png)

Figure 10.16: A bass chorus.

![](img/b54974d0a4317ec82d7ae02126d10a6f_338_0.png)

Figure 10.17: A dimension-style chorus.

The controls on the original unit consisted of four switches only; these were hardwired presets and changed

- The LFO rate (either 0.25 Hz or 0.5 Hz)
- The depth
- For one preset, the wet/dry mix ratios for the two channels ($W_L$ vs $D_L$, $W_R$ vs $D_R$)

Here I have added two more level controls for experimentation, $W_{CL}$ and $W_{CR}$, which are the filtered, inverted chorused signals from the opposite (crossed) channels. Experiment with various rate, depth, and output mixture combinations as well as different high-pass filter cutoff frequencies.

### 10.6.5 Deca-Chorus (Sony DPS-M7®)

The deca-chorus has 10 (deca) chorus units, 5 per channel. Each chorus has its own pre-delay, LFO, gain, and pan control. It can also run in a mono mode (10 chorus units in parallel) (Figure 10.18).

![](img/b54974d0a4317ec82d7ae02126d10a6f_339_0.png)

Figure 10.18: DPS-M7 deca chorus.

## Bibliography

- Cole, M. 2007. “Roland dimension C clone for Eventide 7000, Orville and H8000.” Accessed August 2012 from http://www.eventidstompboxes.com/forummedia/PATCHES/Orville/ProFXalgorithms/Roland%20Dimension%20C.doc.
- Coulter, D. 2000. Digital Audio Processing, Chapter 11. Lawrence, KS: R&D Books.
- Dattorro, J. 1997. Effect design part 2: Delay line modulation and chorus. Journal of the Audio Engineering Society, 45(10): 764–786.
- Korg, Inc. 2000. Triton Rack Parameter Guide. Tokyo: Korg Inc.
- Phillips, D. 1991. Wavestation SR Reference Guide. Tokyo: Korg Inc.
- Roads, C. 1996. The Computer Music Tutorial, Chapter 3. Cambridge, MA: The MIT Press.
- Roland Corporation, 1990. “Boss CH-1 schematics.” Accessed August 2012 from http://superchorusmods.blogspot.com/2009/08/schematics.html.
- Sony, Corp. 1995. DPS-M7 Manual. Tokyo: Sony Corp.
- White, P. 2001. “Understanding and emulating vintage effects.” Sound on Sound Magazine. Accessed August 2012 from http://www.soundonsound.com/sos/jan01/articles/vintage.asp.

## Reverb Algorithms

Reverb algorithms might represent the Holy Grail of audio signal processing. They have an appeal that seems universal, perhaps because we live in a reverberant world. Our ears are time-integrating devices that use time domain cues and transients for information, so we are sensitive to anything that manipulates these cues. In this chapter, we discuss reverb algorithms as applied mainly to room simulation. There are two general ways to create the reverberation effect:

- Reverb by direct convolution—the physical approach.
- Reverb by simulation—the perceptual approach.

In the physical approach, the impulse response of a room is convolved with the input signal in a large finite impulse response (FIR) filter. For large rooms, these impulse responses might be up to 10 seconds. In the mid 1990s, Gardner developed a hybrid system for fast convolution that combined direct convolution with block fast Fourier transform (FFT) processing (Gardner 1995). Around the same time, Reilly and McGrath (1995) described a new commercially available system that could process 262,144-tap FIR filters for convolving impulses over several seconds in length. The required processing power is sometimes too large to be practical in a plug-in. Aside from the computing expense, another drawback to this approach is that an impulse response is frozen in time, and measures the room at one location only, under a certain set of conditions. To create a reverb unit (or reverberator) that is general enough to provide many different reverbs of different spaces would require a large library of impulse response files. In addition, its parameters can't be adjusted in real time.

The perceptual approach aims to simulate the reverberation with enough quality to fool the ears and give the same perception of real reverb but with much less processing power. The advantages are numerous, from the minimal processing required to the ability to vary many parameters in real time. Browne (2001) proposed a hybrid system combining a short impulse response convolution along with recursive filtering, combining both approaches. There are several key engineers who developed much of the theory still in use today. These include Schroeder's (1962) initial work in the early 1960s with continued research and contributions from Moorer, Griesinger, Gerzon, Gardner, Jot, Chaigne, Smith, Roscosso, and others across the decades. Most of this chapter is owed to their work in the field. We will focus on the perceptual approach and try to find computationally efficient algorithms for interesting reverberation effects.

Griesinger (1989) states that it is impossible to perfectly emulate the natural reverberation of a real room and thus the algorithms will always be approximations. It seems that the area of reverberation design has the most empirically derived or trial-and-error research of just about any audio signal processing field. There is no single “correct” way to implement a reverb algorithm, so this chapter focuses on giving you many different reverberator modules to experiment with.

### 11.1 Anatomy of a Room Impulse Response

The first place to start is by examining impulse responses of actual rooms. There are several popular methods for capturing the impulse response, from cap pistols and balloons to deconvolution of chirp signals and pseudo random sequences. The resulting time domain plot is useful for investigating the properties of reverberation.

Figure 11.1 shows the impulse response plots for two very different spaces; a large concert hall and a cathedral. The initial impulse is followed by a brief delay called the pre-delay. As the impulse pressure wave expands, it comes into contact with the nearby structures—walls, floor, and ceiling—and the first echoes appear. These initial echoes, called early reflections, are important to the simulation of reverb because of the auditory cues we get from them. The pressure wave continues to expand and more reflections occur, with reflected signal upon reflected signal piling on top of each other while decaying in energy. The resulting reverb “tail” is called late reverberation or subsequent reverberation.

The top impulse response in Figure 11.1 is a modern concert hall designed for a pleasing reverberant quality. The initial reflections are from irregularly shaped back and side walls and they pile up in amplitude; they are also piling up in density, shown as the impulse gets “fatter” in the middle section. The dense reverberant tail follows, which decays in an exponential fashion, and the sound pressure energy is absorbed by the seats and acoustical room treatments. The cathedral is a different story.

After a short pre-delay, a few large early reflections arrive from the nearby structures but they don’t increase in amplitude or density in the same way as the hall. The reverb’s decay is also much longer in time as there is little in the cathedral to absorb the sound pressure.

The block diagram in Figure 11.2 shows the three components we observe. However, there is debate as to whether or not this is a good way to break the problem down. Some feel that the reverb algorithm should not need to separate out the early reflections from the late reverberation. In other words, a good algorithm will create all of the reverberation aspects at once.

![](img/b54974d0a4317ec82d7ae02126d10a6f_341_0.png)

Figure 11.1: The impulse responses of a large hall and cathedral.

![](img/b54974d0a4317ec82d7ae02126d10a6f_342_0.png)

#### 11.1.1 RT60: The Reverb Time

The most common measurement for reverb is the RT60 reverb time. Reverb time is measured by first stimulating the room into a reverberant state, then turning off the source and plotting the pressure-squared level as a function of time. The amount of time it takes for this energy decay curve to drop by 60 dB is the reverb time, or RT60. Sabine's (1973) pioneering work in this area leads to the following formula in Equation 11.1:

$$RT_{60} = 0.5 \frac{V_R}{S_R A_{Rave}}$$ (11.1)

where

- \(V_R\) = volume of room in ft³
- \(S_R\) = surface area of room in ft²
- \(A_{Rave}\) = average absorption coefficient

Sabine measured and tabulated the absorption coefficients for various materials. The units are given in Sabines. A room made of several materials is first partitioned to find the partial surface area of each material type, then the average is found by weighting the areas with the absorption coefficients and summed. The reverb time is probably the most common control, found on just about every kind of reverb plug-in.

### 11.2 Echoes and Modes

In Schroeder's early work, he postulates that a natural sounding artificial reverberator has both a large echo density and a colorless frequency response. The echo density is simply the number of echoes per second that a listener experiences in a given position in the reverberant environment (Equation 11.2).

$$E_D = \frac{\text{echoes}}{\text{second}}$$ (11.2)

If the echo density is too low the ear discerns the individual echoes and a fluttering sound is the result. As the echo density increases, the echoes fuse together, producing a wash of sound. Schroeder (1962) postulated that for a natural-sounding reverb, the echo density needs to be 1000 echoes/second. Griesinger (1989) increases this to 10,000 echoes/second or more. Statistically, the
