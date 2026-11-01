![](bbox=[0.13, 0.17, 0.78, 0.27])

FIGURE 2-17

4. Position your cursor at the end of the heading after the word Wrox and press Enter. A new paragraph (indicated by a small glyph with the letter p on it) is inserted for you so you can directly start typing.

5. Type the text shown in Figure 2-18 (or make up your own) to welcome the visitor to Planet Wrox. Notice how the text www.PlanetWrox.com turns blue as soon as you type the comma to indicate VS has recognized it as a web address and has turned it into a link. You can press Enter to start a new paragraph. Select the text "paying a visit," click the Foreground Color button on the Formatting toolbar, and select a different color in the dialog box that appears. Then select some other text, such as "reviews and concert pictures," and click the Bold button. When you're done, your Design View should show something similar to Figure 2-18.

![](bbox=[0.13, 0.6, 0.78, 0.72])

FIGURE 2-18

The code for the homepage should now look more or less similar to the following (the code has been reformatted a bit to fit the space in the book):

```
<div>
<h1>Hi there visitor and welcome to Planet Wrox</h1>
<p>
&nbsp;&nbsp;We're glad you're paying a visit to <span class="auto-style1">paying a visit</span> to <a href="http://www.PlanetWrox.com">www.PlanetWrox.com</a>, the coolest music community site on the Internet.
</p>
<p>
&nbsp;&nbsp;Feel free to have a look around; there are lots of interesting <strong>reviews and concert pictures</strong> to be found here.
</p>
</div>
```