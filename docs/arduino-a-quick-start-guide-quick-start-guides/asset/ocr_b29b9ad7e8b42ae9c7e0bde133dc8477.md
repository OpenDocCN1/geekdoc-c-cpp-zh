![](bbox=[0.15, 0.09, 0.75, 0.35])

# Figure 7.4: Message flow between Arduino and Nunchuk

```
void Nunchuk::request_data() {
  Wire.beginTransmission(NUNCHUK_DEVICE_ID);
  Wire.send(0x00);
  Wire.endTransmission();
}

char Nunchuk::decode_byte(const char b) {
  return (b ^ 0x17) + 0x17;
}
```

After including all libraries we need, we define the NUNCHUK_DEVICE_ID constant. I²C is a master/slave protocol; in our case, the Arduino will be the master, and the Nunchuk will be the slave. The Nunchuk registers itself at the data bus using a certain ID (0x52), so we can address it whenever we need something.

In initialize(), we establish the connection between the Arduino and the Nunchuk by sending a handshake. In line 8, we call Wire's begin() method, so the Arduino joins the I²C bus as a master (if you pass begin() an ID, it joins the bus as a slave having this ID). Then we begin a new transmission to the device identified by NUNCHUK_DEVICE_ID: our Nunchuk.