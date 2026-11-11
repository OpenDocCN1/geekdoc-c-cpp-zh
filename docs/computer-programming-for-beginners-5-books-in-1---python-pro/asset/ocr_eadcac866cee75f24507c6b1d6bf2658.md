part of the program.

```
```cpp
// convert the ADC reading to voltage
float voltage = (sensorValue / 1023.0) * 5.0;
```
```

```
```cpp
Serial.print("Volts = ");
Serial.println(voltage);
```
```

```
```cpp
Serial.print(" degrees C ");
// convert the voltage to temperature in degrees
float temperature = (voltage - .5) * 100;
Serial.println(temperature);
```
```

Source: the database