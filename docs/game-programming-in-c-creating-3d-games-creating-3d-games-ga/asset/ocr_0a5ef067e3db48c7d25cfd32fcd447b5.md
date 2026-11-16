cave have an echo because of waves bouncing off the walls. **Equalization**, on the other hand, tries to normalize the volume levels of sounds into a set range.

FMOD Studio allows configuration of chains of DSP effects. In other words, a sound can pass through multiple stages that modify the signal prior to output. Although each sound event can have its own DSP chain, a more common approach is to group sounds into types. Then, different groups can have different effects applied to them.

# Buses

In FMOD Studio, a **bus** is a grouping of sounds. For example, you might have a bus for sound effects, a bus for music, and a bus for dialogue. Each bus can individually have different DSP effects attached to it, and at runtime you can adjust buses. For instance, many games offer separate volume sliders for different categories of sound. This is straightforward to implement with buses.

By default, every project has a master bus, specified by the root path `bus:/`. However, a sound designer can add any number of additional buses. So, much as with loading in event descriptions on bank load, you can load in buses at the same time. First, you add a map of buses to `AudioSystem`:

Click here to view code image

```
std::unordered_map<std::string, FMOD::Studio::Bus*> r
```