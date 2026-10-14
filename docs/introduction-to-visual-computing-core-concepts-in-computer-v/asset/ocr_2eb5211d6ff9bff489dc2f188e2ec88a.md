# 13.4  Conclusion

We learnt about the interactive graphics pipeline in this chapter. We have deliberately kept this treatise API independent and given you the fundamental concepts. We hope that following this you can adapt API specific aspects into the pipeline easily. For example, OpenGL assumes the normal to the image plane in the view set-up to be negative Z. This means the view transformation and the perspective transformation will change slightly and we hope you can work through it. In this chapter we have not given you details about clipping and rasterization methods assuming they will be done in the graphics hardware. To learn more about such techniques, please look up [Foley et al. 90, Shirley and Marschner 09, Watt 99].

# Bibliography

+   - [Foley et al. 90] James D. Foley, Andries van Dam, Steven K. Feiner, and John F. Hughes. *Computer Graphics: Principles and Practice (2nd Ed.).* Boston, MA, USA: Addison-Wesley Longman Publishing Co., Inc., 1990.
+   - [Shirley and Marschner 09] Peter Shirley and Steve Marschner. *Fundamentals of Computer Graphics.* A. K. Peters, Ltd., 2009.
+   - [Watt 99] Alan Watt. *3D Computer Graphics.* Addison Wesley, 1999.