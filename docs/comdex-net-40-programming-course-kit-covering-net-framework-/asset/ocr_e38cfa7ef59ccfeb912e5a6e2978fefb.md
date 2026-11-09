in Silverlight applications. This in turn helps you to make your Web site more user-friendly. The data-binding and data-manipulation controls, such as **DataGrid**, can also be used in Silverlight Web site to retrieve and store data in databases.

# ## Support for Deep Zoom Technology

Silverlight includes a support for a technology called Deep Zoom, which allows you to zoom high-resolution images in Web sites. With the help of the Deep Zoom technology, you can easily zoom in or out multiple images simultaneously. This technology reduces the time required for initial load by downloading only the region being viewed. It also allows you to view thousands of images simultaneously.

# ## Support for 3D Graphics, Animations, and Multimedia

Silverlight has built-in support for 2D vector graphics and animations. In addition, it allows you to create, transform, and animate 2D shapes. However, with the release of Silverlight 3.0, you can perform perspective 3D transformations to create more attractive Web visuals containing new 3D graphics, animation features, and hardware accelerated effects. Perspective transforms are transformations that you can apply on Extensible Application Markup Language (XAML) elements to simulate a 3D environment. You can apply 3D effects to controls in your Silverlight applications by using the attached property, called Projection, within a parent element. Consider the following code snippet:

```
```xml
<Button Height="90" Content="Perspective Transform">
<Button.Projection>
<PlaneProjection RotationY="60"/>
</Button.Projection>
</Button>
```
```

In the preceding code snippet, the Button control is rotated to give it a perspective, with a 60 degree rotation on the Y-axis.

In addition, you can make your Web sites dynamic by using storyboards and controlling the animation timeline and speed. For this, you can include .jpeg or .png extension images in the Web sites. Silverlight also supports various multimedia formats, such as .wma, .wmv, and .mp3, to play multimedia content on the Web site. You can also use High-Definition (HD) quality video (up to 720p) in Silverlight applications.

![](bbox=[0.212, 0.559, 0.277, 0.598])

> > **Vector graphics are shapes and drawing used to represent geometrical images, such as points, lines, curves, and polygons.**

# ## Support for Networking

Silverlight contains classes to support networking and predefined sockets. It allows you to use various services, such as Hypertext Transfer Protocol (HTTP), XML, Really Simple Syndication (RSS), and Representational State Transfer (REST) to develop distributed applications. Silverlight extends the cross-domain support for networking to enable communication with a server.

# ## Support for Higher Quality Video and Audio

Silverlight supports the high quality video and audio. It supports new audio and video formats, such as H.264, Advanced Audio Coding (AAC), and Moving Picture Experts Group (MPEG) 4. In addition, it includes support for live and on-demand Internet Information Services (IIS) 7 Smooth Streaming, full HD (720+) playback, and raw audio or video (AV) pipeline. The raw AV pipeline enables the .NET developers to provide audio/video decoding that can be hosted outside the .NET Framework runtime environment.

# ## Out-of-Browser Capabilities

The Out-of-Browser capability, first introduced with the Silverlight 3.0, enables the Silverlight applications to run either with or outside a Web browser. It means that you can install a Silverlight