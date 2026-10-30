**Namespaces used:**
`Osp::Uix`

**Header files to #include:**
`FUixSensorManager.h, FUixSensorTypes.h`

**Required libraries:**
`FUix`

**Required privilege level:**
`Normal`

**Required privilege groups:**
`None`

This recipe is related to the namespace `Osp::Uix`. Uix stands for UI extension, which provides additional novel ways for the user to interface with a mobile device. These are not covered in basic UIs. Traditional UI approaches mostly depend on oral or visual input and output for providing information, or they take commands or information from the user through buttons. UI extension is intended to improve the user’s experience in interacting with a mobile phone.

This recipe covers one particular part of that namespace. It makes use of the magnetometer (magnetic sensor). This sensor is a three-axis electronic compass that can also be used for determining the orientation. The magnetic sensor measures the magnetic field strength. The measurements are split into the X, Y, and Z axis and the unit is Micro-Tesla (µT). Note that several factors can have an impact on the data coming from this sensor: weather, your current location on the planet, and, most influentially, nearby magnetic fields, such as magnets or electric coils.

The magnetic sensor uses the phone as a fixed frame of reference as indicated in Figure R3.2, and models this into the three-axis Cartesian space coordinate system.

![](bbox=[0.28, 0.84, 0.78, 0.97])

Figure R3.2 Magnetic field related to the device.