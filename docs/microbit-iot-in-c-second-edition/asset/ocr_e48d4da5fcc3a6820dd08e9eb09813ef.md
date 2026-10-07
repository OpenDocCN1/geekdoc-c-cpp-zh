```
int main()
{
    uBit.init();
    uBit.display.setDisplayMode(DISPLAY_MODE_GRESCALE);
    uBit.radio.enable();

    uBit.radio.event.listen(MICROBIT_ID_BUTTON_A,
        MICROBIT_BUTTON_EVT_DOWN);
    uBit.radio.event.listen(MICROBIT_ID_BUTTON_A,
        MICROBIT_BUTTON_EVT_UP);
    uBit.messageBus.listen(MICROBIT_ID_BUTTON_A,
        MICROBIT_BUTTON_EVT_DOWN, beepon);
    uBit.messageBus.listen(MICROBIT_ID_BUTTON_A,
        MICROBIT_BUTTON_EVT_UP, beepOff);

    while (1)
    {
        uBit.sleep(100);
    }
}
```

If you try this out you will need to change P0 to speaker to run on a V2 and make sound on the built-in speaker. You might be surprised that you can redirect the button up and down events on both devices – surely this would create a feedback loop? The reason it doesn't is that each micro:bit forwards by radio only the presses on its buttons. This makes the program a two-way Morse communication device.