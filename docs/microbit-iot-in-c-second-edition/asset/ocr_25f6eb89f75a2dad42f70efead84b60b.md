At the time of writing this program returns zero for all timings on a V2 due to the timestamp of the event object not being set. This bug will probably be resolved some time in the future, a fix is to edit:

libraries/codal-nrf52/source/NRF52Pin.cpp.

Find the NRF52Pin:rise() and NRF52Pin::fall() methods and in both cases change the line:

```
Event(id, DEVICE_PIN_EVT_RISE, 0)
```

to read:

```
Event(id, DEVICE_PIN_EVT_RISE, system_timer_current_us());
```

The program records accurate times for pulses longer than 250µs but starts to miss pulses as the pulse width shortens to 100µs, when it misses about one pulse in ten. If the event handlers take longer to perform their tasks then the limit would be even larger.

Events are great for handling things that happen on the scale of 100s of microseconds and preferably in terms of milliseconds.

Also notice that the documentation says the shortest pulse that can be reliably detected, i.e. will fire a MICROBIT_PIN_EVENT_ON_PULSE event, is 85µs.

Events are only useful if the time that the event handler takes, plus the overheads of servicing an event, is less than the average repetition rate of the event.