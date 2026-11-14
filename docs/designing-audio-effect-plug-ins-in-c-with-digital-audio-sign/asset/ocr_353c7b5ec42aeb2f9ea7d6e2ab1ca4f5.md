```
// Stereo-In, Stereo-Out (INSERT Effect)
if((uNumInputChannels == 2 && uNumOutputChannels == 2)
pOutputBuffer[1] = fDepth*fAPF_6_Out + (1.0 - fDepth)
*pInputBuffer[1];
return true;
}
```

Build and test the plug-in. Try out the different modes; turn up the intensity and depth controls for very intense effects. This phaser should be one of the finest you have heard as it is not like some digital phasers that only use one giant APF. The cascaded APFs are the way to go with this effect. The saw LFO with copious feedback sounds very much like a classic pulsating “vibe” effect.

# Bibliography

+   Anderton, C. 1981. Electronic Projects for Musicians. London: Wise Publications.
+   Dodge, C. and Jerse, T. 1997. Computer Music Synthesis, Composition and Performance. Chapter 2. New York: Schirmer.
+   Giles, M., ed. 1980. The Audio/Radio Handbook. Santa Clara, CA: National Semiconductor Corp.
+   Roads, C. 1996. The Computer Music Tutorial. Chapter 2. Cambridge, MA: The MIT Press.

# References

+   musicdsp.org. “Envelope follower with different attack and release.” Accessed 2008, http://www.musicdsp.org/archive.php?classid=0#205.
+   Orfanidis, S. 1996. Introduction to Signal Processing, Chapter 8. Englewood Cliffs, NJ: Prentice-Hall.
+   Zölzer, U. 2011. DAFX—Digital Audio Effects, Chapter 4. West Sussex, U.K.: John Wiley & Sons.