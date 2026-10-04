+   2. Next, make sure that you have at least two browsers set as the default. Browser Link works with a single browser as well but its usefulness increases with each additional browser you open. You can select multiple browsers by clicking the down arrow next to the name of the current default browser on the Standard toolbar, as explained earlier.

+   3. Open Default.aspx from the root of the site in Markup View and press Ctrl+F5 to open the site in your configured browsers.

+   4. Organize the open browsers and Visual Studio so you can see them all side by side, as shown in Figure 18-31.

![](bbox=[0.16, 0.29, 0.82, 0.67])

FIGURE 18-31

+   5. Switch back to Visual Studio and make a change to the code. For example change the text in the <h1> element back to welcome to Planet Wrox.

+   6. Press Ctrl+Alt+Enter or choose Refresh Linked Browsers from the Browser Link menu. Your open browsers should now reload and display the new content. If nothing happens, check the Browser Link Dashboard for any issues preventing Browser Link from working, and follow the instructions to fix them. Then close your browsers and restart this exercise at step 3.

# How It Works

When you start the browsers with Browser Link enabled, a link to some JavaScript is appended to the page. This script sets up a communication channel between Visual Studio and the connected browsers. When you press Ctrl+Alt+Enter in Visual Studio, it sends a notification to the browsers that they should reissue a request for the page to the server to show the latest changes.