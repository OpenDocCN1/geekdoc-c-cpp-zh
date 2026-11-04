```
```csharp
SoundBuffer3D = new Buffer3D(SoundBuffer);
SoundBuffer.Play(0, BufferPlayFlags.Default);
SoundBuffer3D.Position = new Vector3(-0.2f, 0.0f, 1.0f);
...
SoundBuffer = new SecondaryBuffer(MEDIA_ROOT + "Racket.wav", sound);
EffectDescription[] effects = new EffectDescription[1];
effects[0].GuidEffectClass = DSoundHelper.StandardGargleGuid;
SoundBuffer.SetEffects(effects);
SoundBuffer.Play(0, BufferPlayFlags.Default);
...
```
```

| Effect: | Description: |
|---|---|
| Chorus | A voice-doubling effect, the original sound is repeated after a short delay. The sound is also slightly altered, creating the illusion of multiple voices. |
| Compression | A reduction in the fluctuation of amplitude as it is measured from the signal's average. |
| Distortion | An abrupt slicing of the top of a waveform created by adding harmonics to the signal as the level increases. |
| Echo | Sounds are repeated after a fixed delay, usually at a diminished volume. This process repeats for several cycles. |
| Environment Reverberation | An implementation of the listener properties; a sound reaching the listener has three temporal components: direct path, early reflections, and late reverberation. The combination of early reflections and late reverberation is also referred to as the room effect. |
| Flange | Also known as flanger, an echo/sweeping effect, which includes a shorter delay and some variance. |
| Gargle | An intonation/modulation of a signal's amplitude meant to causes a unique sound. |
| Parametric Equalizer | Used to amplify or attenuate a signal, allowing for different pitches that can be applied in parallel. |
| Waves Reverberation | Intended for use with music, the wave's reverberation DirectX Media Object (DMO) is based on the wave's MaxxVerb technology. |

Table 4.8