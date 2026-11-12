Simply put, ray tracing is one way of producing a two-dimensional image of a scene consisting of three-dimensional objects. But isn’t this what GPUs were originally designed for? How is this different from what OpenGL or DirectX do when you play your favorite game? Well, GPUs do indeed solve this same problem, but they use a technique known as rasterization. There are many excellent books on rasterization, so we will not endeavor to explain the differences here. It suffices to say that they are completely different methods that solve the same problem.

So, how does ray tracing produce an image of a three-dimensional scene? The idea is simple: We choose a spot in our scene to place an imaginary camera. This simplified digital camera contains a light sensor, so to produce an image, we need to determine what light would hit that sensor. Each pixel of the resulting image should be the same color and intensity of the ray of light that hits that spot sensor.

Since light incident at any point on the sensor can come from any place in our scene, it turns out it’s easier to work backward. That is, rather than trying to figure out what light rays hits the pixel in question, what if we imagine shooting a ray from the pixel and into the scene? In this way, each pixel behaves something like an eye that is “looking” into the scene. Figure 6.1 illustrates these rays being cast out of each pixel and into the scene.

![](bbox=[0.28, 0.56, 0.71, 0.81])

Figure 6.1 A simple ray tracing scheme