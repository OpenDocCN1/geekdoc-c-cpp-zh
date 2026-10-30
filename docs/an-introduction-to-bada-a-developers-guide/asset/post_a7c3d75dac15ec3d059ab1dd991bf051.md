
![](img/a257d5fd53a79a244a20e587cd2f08f6_350_0.png)

This behaviour should be considered when designing an application’s response to both motion and touch events.

## Related Recipe
- Add a Form to a Frame-based App

## Recipe 3.2: Get Device Orientation from the Magnetometer (Compass)

### Problem Description
You want to obtain data from the magnetometer (compass sensor) to interpret that information for various applications (e.g. determine device orientation or metal detection).

### The Recipe
The following configuration is required for this recipe:

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

![](img/a257d5fd53a79a244a20e587cd2f08f6_351_0.png)

Figure R3.2 Magnetic field related to the device.

For this example we use the SensorManager class and the ISensorEventListener interface, both from the namespace Osp::UiX. The SensorManager class provides the functionality for adding and removing sensor listeners, checking if a sensor is available, setting intervals, and getting the maximum and minimum intervals. A bada device can have various physical sensors (e.g. an acceleration sensor or proximity sensor). The SensorManager supports simple access to built-in sensors in a device. By registering a listener to the SensorManager, an application can get sensor data with a timestamp based on definable intervals.

In our example we define a class that inherits from the ISensorEventListener interface. Below is a sample header file that contains all the signatures for the methods we show in this recipe.

```
//...
class YourClassName :
{
    public Osp::UiX::ISensorEventListener

private:
    Osp::UiX::SensorManager sensorMgr;
    // ...

public:
    // ...
    bool RegisterSensor();
    bool UnRegisterSensor();
    void OnDataReceived(Osp::UiX::SensorType sensorType,
        Osp::UiX::SensorData& sensorData, result r);

private:
    void DrawArrow();
    float GetDegree(float rad);
    float CalculateAngle(float f1, float f2);
};
```

Because we inherit from an interface, we need to overwrite the respective method with the following signature:

```
void OnDataReceived(Osp::UiX::SensorType sensorType,
Osp::UiX::SensorData& sensorData, result r);
```

The implementation of our class also provides two methods that help to register and unregister a sensor type.

```
bool
RegisterSensor()
{
    result r = E_SUCCESS;

    // Construct the sensor manager instance
    r = sensorMgr.Construct();
    if(IsFailed(r))
{
    return false;
}
long interval = 0;

// Activate the sensor type SENSOR_TYPE_MAGNETIC
r = sensorMgr.GetMinInterval(SENSOR_TYPE_MAGNETIC, interval);
if(IsFailed(r))
{
    return false;
}
if (interval < 50)
{
    interval = 50;
}
// Register our listener to this sensor
r = sensorMgr.AddSensorListener(*this, SENSOR_TYPE_MAGNETIC, interval, false);
if(IsFailed(r))
{
    return false;
}

return true;
}

bool
UnRegisterSensor()
{
    result r = E_SUCCESS;

    // Deactivate our compass sensor
    r = sensorMgr.RemoveSensorListener(*this);
    if(IsFailed(r))
    {
        return false;
    }
    return true;
}
```

In the body of the overwritten OnDataReceived() method we get the X, Y, and Z values and can process them as needed. In this example we simply calculate the 3D vector of the Earth’s magnetic field (assuming that there are no other sources of severe interference). For this purpose we have defined a member of type float called magField into which we store the length of this vector.

```
void
OnDataReceived(Osp::UiX::SensorType sensorType, Osp::UiX::SensorData&
sensorData, result r)
{
    float x=0, y=0, z=0;

    AppLog("DataReceived: Get Magnetic Sensor Data");

sensorData.GetValue({SensorDataKey}MAGNETIC_DATA_KEY_X, x);
sensorData.GetValue({SensorDataKey}MAGNETIC_DATA_KEY_Y, y);
sensorData.GetValue({SensorDataKey}MAGNETIC_DATA_KEY_Z, z);

// Calculate the length of our vector determined by the three axis
magField = Math::Sqrt((Math::Pow(x,2)+ Math::Pow(y,2)+
Math::Pow(z,2)));
}
```

### Hints, Pitfalls, and Related Topics
Once your code compiles without errors, you can run it in the Simulator. A very convenient feature of the bada Simulator is the Event Injector tool. To get this, right-click the Simulator screen, select the Event Injector, and choose the Sensors tab. In the row below choose the Magnetic tab. There you can freely choose the μT values per X, Y, and Z axis. Click on the Send button to send these as events to your application running on the bada Simulator. This tool is very useful for testing.

For some use-cases you might be interested in getting the angle between two vectors. The following code snippet should help:

```
float
CalculateAngle(float f1, float f2)
{
    float angle = 0;
    // angle in rad
    if (f1==0 && f2==0){
        angle = 0;
        return angle;
    }else{
        angle = Math::Asin(f1 / Math::Sqrt((Math::Pow(f1,2) +
        Math::Pow(f2,2))));
    }
    return angle;
}
```

The SDK calculates the angle in rad. For converting this into degrees you may find the following code useful:

```
float
GetDegree(float rad)
{
    return Math::Abs(rad * 180/Math::GetPi());
}
```

## Recipe 3.3: Get Readings from the Tilt Sensor

### Problem Description
You want to make use of the azimuth, pitch, and roll values from tilt sensor and display them on the screen.

### The Recipe
The following configuration is required for this recipe:

Namespaces used:
Osp::UI, Osp::UI::Controls, Osp::UIx

Header files to #include:
FUI.h, FUIx.h

Required libraries:
FUI, FUIControls, FUIx

Required privilege level:
None.

Required privilege groups:
None

The tilt sensor measures the angle of your mobile device at each position. The sensor combines acceleration and magnetic sensor to determine values of azimuth, pitch, and roll (see Figure R3.3). The range of values that the tilt sensor supports are shown in Table R3.1.

### Table R3.1 Range of values supported by the tilt sensor

| Measurement | Type | Range | Unit |
|---|---|---|---|
| Timestamp | long | – | Milliseconds |
| Azimuth | float | Max. value = 360 Min. value = 0 | Degrees (°) |
| Pitch | float | Max. value = +180 Min. value = -180 | Degrees (°) |
| Roll | float | Max. value = +180 Min. value = -180 | Degrees (°) |

These are angular positions based on a fixed frame reference.

![](img/a257d5fd53a79a244a20e587cd2f08f6_356_0.png)

Figure R3.3 Azimuth, pitch and roll.

In this recipe we are going to:
- 1. Construct a base Form and Label.
- 2. Construct the SensorManager and add the required listener for tilt sensor.
- 3. Inherit from the ISensorEventListener interface.
- 4. Implement the OnDataReceived() method.

As a result, the values of the tilt sensor will be displayed on the screen (see Figure R3.4).

![](img/a257d5fd53a79a244a20e587cd2f08f6_356_1.png)

Figure R3.4 Values of the tilt sensor on the Simulator.
