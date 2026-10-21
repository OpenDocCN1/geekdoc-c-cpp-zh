# Arduino Arts

You can use the Arduino not just for gadgets or fun projects but also in artistic ways. Especially in the new-media art area you will find many amazing projects built with the Arduino. One of them is Anthros,* a responsive environment that observes a small area using a webcam. The area contains some “tentacles,” and whenever a person crosses the area, the tentacles move into the person’s direction. Servos move the tentacles, and an Arduino controls the servos.

For all people interested in new-media art, Alicia Gibb’s thesis “New Media Art, Design, and the Arduino Microcontroller: A Malleable Tool”† is a must-read.

+   * http://www.michiganbank.com/anthros
+   † http://aliciagibb.com/thesis/

someone directly, you can tell the Blaminatr to do so. In Figure 10.5, on the following page, you can see the device in action. Tell it to blame me, and it moves an arrow, so it points to “Maik.”

Blaminatrs are perfect office toys that you can use in many situations. For software developers, it can be a good idea to attach one to your continuous integration (CI) system. Continuous integration systems such as CruiseControl.rb³ or Luntbuild⁴ help you continuously check whether your software is in good shape.

Whenever a developer checks in changes, the CI automatically compiles the software and runs all tests. Then it publishes the results via email or as an RSS feed. You can easily write a small piece of software that subscribes to such a feed. Whenever someone breaks the build, you’ll find a notification in the feed, and you can use the Blaminatr to point to the name of the developer who has committed the latest changes.⁵

In the previous section, you learned all about servo motors you need to build the Blaminatr. Now we only need some creativity to build the device’s display, and we need more elaborate software. We start with

+   3. http://cruisecontrolrb.thoughtworks.com/
+   4. http://luntbuild.javaforge.com/
+   5. At http://urbanhonking.com/ideasfordozen/2010/05/19/the_github_stoplight/, you can see an alternative project. It uses a traffic light to indicate your project’s current status.