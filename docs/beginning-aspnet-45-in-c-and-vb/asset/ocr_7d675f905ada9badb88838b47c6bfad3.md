+   1. Open up the Frontend.master file from the MasterPages folder and make sure it's in Markup View.
+   2. Near the bottom of the page, right before the closing </form> tag, drag a ContentPlaceHolder from the Toolbox. Set its ID to cpClientScript. Your code should end up like this:
+   ```html
+   <footer>Footer Goes Here</footer>
+   </div>
+   <asp:ContentPlaceHolder ID="cpClientScript" runat="server">
+   </asp:ContentPlaceHolder>
+   </form>
+   ```
+   3. Save and close the master page because you're done with it for now.
+   4. Create a new demo page called BasicSelectors.aspx in the Demos folder. Once again, base it on your own template and give it a meaningful title. Switch the page to Design View, locate the cpClientScript placeholder at the bottom, open its Smart Tasks panel, and choose Create Custom Content.
+   5. Switch to Markup View and add the following HTML to the cpMainContent placeholder (don't accidentally add it to the placeholder you just added):
+   ```html
+   <h1>Basic Selectors</h1>
+   <div class="SampleClass">I am a div.</div>
+   ```
+   6. Add the following jQuery code demonstrating all six basic selectors to the cpClientScript placeholder you created in step 4:
+   ```html
+   <asp:Content ID="Content3" runat="server" ContentPlaceHolderID="cpClientScript">
+   <script type="text/javascript">
+   $(function()
+   {
+   $(' * ').css('color', 'Green');          // Universal
+   $('#sidebar').css('border-bottom', '2px solid red');   // ID
+   $('h1').bind('click', function() { alert('Hello World') });   // Element
+   $('.SampleClass').addClass('PleaseWait').hide(5000);   // Class
+   $('footer, header').slideUp('slow').slideDown('slow');   // Grouped
+   $('#sidebar img').fadeTo(5000, 0.1);   // Combined
+   });
+   </script>
+   </asp:Content>
+   ```
+   7. Save all your changes and request the page in the browser. All text is now green, the sidebar has an extra bottom border, you see the Please Wait animated icon and text appear and then disappear, the header and footer disappear and then reappear, and finally, during a five-second period, the banner in the sidebar becomes almost transparent. If you click the Basic Selectors heading you get a pop-up saying Hello World.

# How It Works

Phew, lots of animation fun. I typically don't recommend adding all these features to your pages at once or you'll be sure to scare away most of your users. However, for this demo it works really well because you can see some of the power of jQuery. You've seen all of the six selectors, but the code that is being executed against their matched sets is probably new to you.