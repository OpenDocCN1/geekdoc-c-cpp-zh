```
}
}
```

In this chapter's game project, there are three buses in all: master, SFX, and music. The sound effects, including footsteps, the fire loop, and the explosion sound, go through the SFX bus, while the background music goes through the music bus.

# Snapshots

In FMOD, **snapshots** are special types of events that control buses. Because they're just events, they use the same event interface that already exists, and the existing `PlayEvent` function works with them. The only difference is that their paths begin with `snapshot:/` instead of `event:/`.

Note that the game project in this chapter uses a snapshot to enable reverb on the SFX bus. Use the `R` key to enable or disable reverb.

# Occlusion

Imagine living in a small apartment when there's a party next door. The music at the party is very loud and travels through your wall. You've heard the song before, but it sounds different when listening through the wall. The bass is more dominant, and it's tough to hear the high-frequency parts. This is