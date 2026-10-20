
![](img/544d515106a3758d5f58491594755dce_107_0.png)

Figure B.5: Safari’s Web Inspector

![](img/544d515106a3758d5f58491594755dce_107_1.png)

Figure B.6: Stepping in Web Inspector

or simply the Esc key to toggle the console on and off, regardless of your currently visible section).

In the current public release of Safari, Web Inspector differs from Firebug in a few key places; for instance, you cannot exactly remove a breakpoint. You can only disable it. You cannot put a condition to it, either. And there are no watches. Still, it’s already a pretty useful tool (and upcoming releases only get better). You can see what stepping looks like a few levels down in the recursion stack, as shown in Figure B.6, which shows how similar its behavior is to Firebug’s.

![](img/544d515106a3758d5f58491594755dce_109_0.png)

# Figure B.7: Visual Web Developer 2008 Express edition: Welcome

There are essentially two rules we must abide by here:

+   - We must have a VWDE project set up and with debugging enabled.
+   - We must set IE7 as our default browser so that it is the one launched by the “Start debugging” feature.

Both requirements need only be dealt with once (unless you’re testing this on the machine where you also surf on a regular basis and therefore need to switch your default browser back and forth between IE and whatever elected browser you have). Let’s address these requirements:

+   1. Open IE6 or IE7, and click Tools > Internet Options....
+   2. Go to the Advanced tab, and scroll to the Browsing section.
+   3. Make sure “Display a notification about every script error” is checked and both “Disable script debugging...” are unchecked.
+   4. Close IE entirely.
+   5. Click File > New Web Site....

![](img/544d515106a3758d5f58491594755dce_110_0.png)

# Figure B.8: Debugging IE7 with breakpoints

+   6. Select the Empty Web Site option, and browse to whatever dummy directory you want to set it up in. Click OK.
+   7. Click the “Start debugging” menu option or icon (the green arrow).
+   8. This first time around, VWDE detects your project is not yet set up for debugging. It lacks a special Web.config file. A dialog box offers to create it for you or continue without debugging—obviously, leave the first option checked, and click OK.
+   9. You should see a development server on a dynamic port started in the taskbar, and your IE opens up on an empty directory listing named after your project’s directory (a warning bar may tell you the browser is working using the Intranet security zone, which is fine with us). You’re set to go!

Now that we’re all set up, just browse to our debugbench.html file any which way. Once opened, look into VWDE. On the right, in the Solution Explorer panel, you should see a Running documents branch with debugbench.html and debugbench.js listed. Double-click the latter.

You’re there! You can now set your breakpoint on line 2 the usual way (click in the gutter), switch back to your IE, and click the Fibo(20) button. You drop back to the debugger in stepping mode, as shown in Figure B.8. Voila!

# B.5 IE8 and Developer Tools

There’s no question about it: Internet Explorer 8 is a great step forward in the IE world. Aside from the notable improvements in web standards support (although it still lags far behind modern browsers, it’s certainly not stuck in the Cretaceous anymore), these points are of immediate interest to us JavaScripters:

+   - The JScript engine in IE8 is on average seven times slower than other JavaScript engines in released browsers. This peaks at a factor of almost twelve against Chrome’s v8 or the latest builds of Safari’s Squirrelfish Extreme and Firefox’s Tracemonkey.
+   
+   Why is that a good news? IE7 used to be up to *ninety times* slower. And IE6 couldn’t live with the shame of its own factor figure. So, the IE team managed to improve its JScript engine by a factor of about thirteen, which has to be declared awesome, like it or not.

+   - The DOM performance in IE8, which is our second major pain point when scripting, has also received some significant love and is now lagging by an average factor of “only” four, which is also a major improvement.

+   - IE8 has built-in “Developer Tools,” which are a cleaned-up, snappier version of the IE Developer Toolbar we use in IE6 and IE7, with an actual *JavaScript debugger* thrown in. One that actually works and doesn’t entail incessant glitches between IE and an external debugging app.

So, not only can we start thinking about reenabling our fancy effects and Ajax operations in the IE world, but we can also do so knowing debugging got a whole lot easier!

Incidentally, IE8 also explores ways to reduce the perceived performance impact of script loading. You still should use generic optimizations such as “load scripts at the bottom of the ”³ and, even more importantly, script concatenation (for example, through Sprockets⁴) and gzip’ping.⁵

The IE8 Developer Tools pane with its Script tab opened and a debugging session going on is shown in Figure B.9, on the following page, with our now-familiar breakpoint. Toggling the debugger on and off is simply a matter of clicking the large button in the toolbar, and we get the usual stepping

3. http://developer.yahoo.com/performance/rules.html#js_bottom
4. http://getsprockets.com
5. For lots of great advice about web page loading and rendering performance, get Thomas Fuchs and Amy Hoy’s excellent *JavaScript Performance Rocks!* [HF09], and check out the Performance tips on the Yahoo! Developer Network at http://developer.yahoo.com/performance/rules.html.

![](img/544d515106a3758d5f58491594755dce_112_0.png)

Figure B.9: IE8 Developer Tools: Script tab

options, local variables, watches, callstack inspection, a sort of console (I wish Microsoft would stop calling those “immediate window”...), and break-points we can disable or remove (no conditions on them, though).

That’s all we need, really! The whole thing feels responsive and never froze my IE8. Honest!

# B.6  Opera and Dragonfly

Opera takes an uncommon approach to providing developer tools. Its Dragonfly tool is “both offline and online,” because it is automatically downloaded and updated through the Internet when you open its pane in Opera. This means you need to be online the first time you use it, which should hardly be an issue. However, in my personal experience, I found it to kind of require being online to simply work. When offline, even if I had downloaded it before, it usually aborted launch because it was not able to connect to Opera’s server (or something).

Its current version (alpha 3 at the time of this writing) clearly states it’s still rough, and I can only hope the Opera folks will come to their senses, UI-wise, and rethink their gazillions-of-multilevel-tabs approach from the ground up. I would think all the other tools use a Firebug-like layout for a reason (it’s simple enough yet powerful enough), but Opera goes on and builds this complex, intricate UI. It seems to have been getting better in recent versions, though.

For our purpose of debugging JavaScript, we just need what’s in the Scripts tab, as displayed in Figure B.10, on the next page. You’ll find toolbar buttons for the usual stuff: run/resume, step over, step into, step out, and when to automatically trigger debug mode (for example, entering a function, encountering an error). A drop-down list lets you display the source file (JavaScript or HTML) you want to debug through; the gutter next to the code lets you deal

![](img/544d515106a3758d5f58491594755dce_113_0.png)

Figure B.10: Opera Dragonfly: Scripts tab

with breakpoints (right-click them to disable/reenable them); the Command line subtab under the code (yes, under...) provides a command line akin to the console; and righthand tabs provide access to the call stack and the local variables (in the Inspection tab).

In short, regular debugging can be done. I should confess, though, that my usual debugging cycle goes like this. First, code with either Safari or Firefox. Then verify and adjust (if needed) in “the other one” (either Firefox or Safari) and then in IE8, IE7, and IE6 (in that order). Finally, just to be sure, run a quick check in Opera and Chrome.

Thus, I follow the sequence I use for XHTML/CSS development. And just like markup and styling, once you get JavaScript working all right in Safari, Firefox, and the IE set, it usually works like a charm in Chrome and Opera. So, debugging in Opera is a rare need for me.

As a final note, know there is a Debug menu you can enable in Opera that gives you direct access to a number of functions reminiscent of Firefox’s Web Developer Toolbar extension or Safari’s Development menu. You can enable it by downloading a configuration file from within Opera.⁶

# B.7 Virtual Machines Are Your Friends

Nowadays RAM is cheap. Most of use web developers code on machines with 4GB to 8GB of RAM, and the even more fortunate guys also run on

6. http://dragonfly.opera.com/app/debugmenu/DebugMenu.ini
