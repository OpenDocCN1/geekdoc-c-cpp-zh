```
foreach (DeviceObjectInstance d in joystick.Objects) {
    if ((0 != (d.ObjectId & (int)DeviceObjectTypeFlags.Axis))) {
        joystick.Properties.SetRange(ParameterHow.ById,
            d.ObjectId, new InputRange(-1000, 1000));
    }
}

joystick.Acquire();
joystick.Poll();
JState = joystick.CurrentJoystickState;

player.direction = 0;

bool Joystick = false;

if (-400 < JState.X) {
    player.direction = AnimatedImage.WEST;
    Joystick = true;
} else if (-500 > JState.X) {
    player.direction = AnimatedImage.EAST;
    Joystick = true;
}

if (Joystick) {
    for(int i = 0; i < 3; i++) {
        player.Animate();
        player.ConstrainToBox();
    }
    Invalidate();
}

byte[] buttons = JState.GetButtons();
foreach (byte b in buttons) {
    if (0 != (b & 0x80)) {
        for (int i = 0; i < NUM_MISSILES; i++) {
            if (playerMissiles[i].isActive == false &&
                player.isActive) {
                FireMissile();
                break;
            } else if (!player.isActive)
                player.isActive = true;
        }
    }
}
```