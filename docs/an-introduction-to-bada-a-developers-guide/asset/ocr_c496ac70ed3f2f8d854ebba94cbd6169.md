# 4.1.3 The Layered Model of the bada Platform

Conceptually, the bada platform is described in terms of four layers. While application developers really only need to know the details of the top layer in order to create applications, it is useful to know more about the platform, how it’s designed and the potential it offers. The four-layer model is shown in Figure 4.1 and we’ll explain what’s contained in each layer below.

![](bbox=[0.25, 0.31, 0.75, 0.65])

Figure 4.1 The bada architecture, a four-layer view.

At the very top of the Figure 4.1 you’ll notice that there are boxes representing three kinds of bada applications: device applications that run stand alone on the device, service applications that make use of the collaboration features of the bada Server (which we’ll explain in more detail later), and web-based and Adobe Flash® applications that the bada framework also supports through its standard controls. Your application could actually be some combination of all three types.

The Framework layer consists of the APIs available to application developers, divided into the 20 top-level namespaces that are explained throughout this book and in detail in Chapter 6. These C++ APIs are the developer’s gateway to the functionality of the device. Here you’ll find the classes for implementing the architecture of an application, storing and restoring application state, supporting basic data types, and accessing system features such as the battery level. The namespaces also include classes for creating the application’s UI, 2D and 3D graphics and taking advantage of the multimedia features of the device. Through these APIs, developers can play and record audio and video, and access the camera, as well as take advantage of the motion, vibrator, and other sensors. It’s also home to the location namespace, which makes including a fully functional map control in your application really simple.