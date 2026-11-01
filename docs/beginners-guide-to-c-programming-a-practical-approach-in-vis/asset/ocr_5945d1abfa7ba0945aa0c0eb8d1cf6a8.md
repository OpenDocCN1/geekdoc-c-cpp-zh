![](bbox=[0.4, 0.1, 0.6, 0.25])

Figure 5.75. The ListBox is populated by even numbers after successive changes in the NumericUpDown’s value

# 5.14. PictureBox

PictureBox is used for displaying images. The image to be shown in a PictureBox is either set during the development or programmatically at runtime. The main properties of a PictureBox are as follows:

+   - **Image**: Used for setting the image to be displayed.
+   - **SizeMode**: Sets how the image will be inserted inside of the PictureBox. It has three frequently used options: **Normal**, **Stretch** or **CenterImage**.

Let’s develop a simple example in which the SizeMode of an image is set by clicking the respective buttons:

+   1. Create a new C# project in Visual Studio.
+   2. Place a PictureBox and three Buttons on the form as follows:

![](bbox=[0.3, 0.85, 0.7, 0.95])

Figure 5.76. Layout of the form