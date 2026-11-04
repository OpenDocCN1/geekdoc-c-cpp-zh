```
missiles[i].imagePosY = player.imagePosY;

TimedEvent missileEvent = timer.getEvent("playerMissile" + i);
missileEvent.Reset();

try {
    SoundBuffer = new SecondaryBuffer(MEDIA_ROOT + "Fire.wav",
        sound);
    SoundBuffer.Play(0, BufferPlayFlags.Default);
} catch {
    Utils.PlaySound(MEDIA_ROOT + "Fire.WAV");
}
break;
}
}
```

# Example 3.54. Animating weapons.

```
public void MoveMissile(TimedEvent e, Object obj) {
    if (gameState.currentState == GameState.State.Stopped) {
        e.isActive = false;
        return;
    }

    AnimatedImage missile = (AnimatedImage) obj;
    if (!missile.isActive) {
        e.isActive = false;
    }

    for (int i = 0; i < gameState.currentSpeed; i++) {
        missile.Animate ();
        missile.WrapinBox ();
        CheckMissileCollision (missile);
    }

    if (e.tickCounter <= 1)
        missile.isActive = false;
```