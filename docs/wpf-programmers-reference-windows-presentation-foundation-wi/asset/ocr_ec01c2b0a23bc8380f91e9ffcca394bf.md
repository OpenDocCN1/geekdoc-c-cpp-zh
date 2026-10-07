This long line of text includes <b>boldbold</b>, <i>italicitalic</i>, and <u>Underlinedunderlined</u> text.
<LineBreak/>

Here's a button:
<InlineUIContainer>
<Button Content="Click Me"/></n</InlineUIContainer>
You even give it a Click event handler.
<LineBreak/>

Here's a really <Run FontSize="20" FontWeight="Bold"&gt;BIG&lt;/Run> word.
<LineBreak/>

This Hyperlink goes to the
<Hyperlink NavigateUrl="http://www.vb-helper.com"&gt;VB Helper site&lt;/Hyperlink>
although it won't work unless you run it inside a navigation host or code-behind.</TextBlock>

The example program UseTextBlock uses this code to produce the TextBlock on the right in **Figure B-1**. The TextBlock on the left displays the same content but the TextWrapping property set to NoWrap.

![](bbox=[0.613, 0.497, 0.903, 0.652])

FIGURE B-1

# TOOLTIP

As you can probably guess, the ToolTip displays a tooltip (see Figure B-13). Usually it's easier to simply set the control's ToolTip property than it is to create a ToolTip object. One in which you might want to make the ToolTip a separate object is if you want to change its properties.

# CONSISTENT TIPS

If you change the ToolTip's properties, you will make it look different from other applications' tooltips. While that will make your program less consistent with the rest of the system, it won't distract the user too much as long as you don't go overboard (e.g., by displaying tooltips in a 60-point font).