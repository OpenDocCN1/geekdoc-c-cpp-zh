The FaceDetector is the class used to locate a face in a still image or camera preview, while the FaceRecognizer will analyse this image and try and identify it from a list of already identified faces.

A device can contain many sensors available to application developers, including acceleration, magnetic, proximity, and tilt sensors. The SensorManager class is used to determine whether a sensor is available and to add or remove the sensor event handlers, while the SensorData class is used to retrieve information from that sensor. The classes that handle the functionality of these sensors are shown in Figure 6.35

![](bbox=[0.28, 0.36, 0.78, 0.68])

Figure 6.35 Sensors provided by the Osp::Ui:: namespace.

> Note: Sensor monitoring methods such as ISensorEventListener::OnDataReceived are called from a separate thread to the main thread, so that they are not slowed down by the API calls in the main thread. This means that if you implement monitoring of a sensor, you should minimise what you do in the OnDataReceived method and do any drawing in the main thread. This also applies to the weather services classes, including WeatherSensor and WeatherForecast, which are used to retrieve weather data for a given location.

Osp::Web

# Declared In:

FWeb.h