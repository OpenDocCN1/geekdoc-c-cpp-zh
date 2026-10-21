```
int get_axis(const int axis) {
    delay(1);
    buffer[axis][buffer_pos[axis]] = analogRead(PINS[axis]);
    buffer_pos[axis] = (buffer_pos[axis] + 1) % BUFFER_SIZE;

    long sum = 0;
    for (int i = 0; i < BUFFER_SIZE; i++)
        sum += buffer[axis][i];
    return round(sum / BUFFER_SIZE);
}

int get_x() { return get_axis(0); }
int get_y() { return get_axis(1); }
int get_z() { return get_axis(2); }

void loop() {
    Serial.print(get_x());
    Serial.print(" ");
    Serial.print(get_y());
    Serial.print(" ");
    Serial.print(get_z());
    Serial.print(" ");
    if (button.update())
        Serial.println(button.read() == HIGH ? "1" : "0");
    else
        Serial.println("0");
}
```

As in Section 3.7, Building a Dice Game, on page 80, we use the Bounce class to debounce the button. The rest of the code is pretty much standard, and the only thing worth mentioning is that we use a 19200 baud rate to transfer the controller data sufficiently fast.

Compile and upload the code, open the serial terminal, and play around with the controller. Move it, press the button sometimes, and it should output something like the following:

```
324 365 396 0
325 364 397 0
325 364 397 1
325 364 397 0
325 365 397 0
325 365 397 1
326 364 397 0
```

A homemade game controller is nice, but wouldn’t it be even nicer if we also had a game that supports it? That’s what we will build in the next section.