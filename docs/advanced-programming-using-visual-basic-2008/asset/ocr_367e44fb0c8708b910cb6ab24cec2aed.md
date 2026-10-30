# Run the Application

STEP 1: Press F5 to run and select the option to modify the Web.config file to allow debugging. Your page should appear in a browser window.

STEP 2: Resize the width of the browser window (Figure 7.26). Because you used percentages for the width of each DIV, the text reflows to fit in the current width. If you wish, you can try changing the font size used by the browser to see how that will affect your page.

The completed page in a browser window.

# Figure 7.26

![](bbox=[0.22, 0.32, 0.78, 0.7])

# Master Pages and Content Pages

A well-designed Web site should have a consistent look from page to page. Master pages provide the ability to define a standard layout and behavior that you use for all of the pages in an application. At run time, the individual content pages merge with the master page to produce the final layout for each page. A great advantage of using master pages is that you can make updates in a single location.

The master page is an ideal location to place the company logo and navigation controls for your site. A ContentPlaceHolder on the master page reserves a space for the content that changes from page to page. A single Web site can have multiple master pages and a given master page can have multiple content place holders.

When a Web site uses master pages, an extra step is required to display a content page. When a browser requests a content page, the content page is retrieved. ASP.NET then checks to see if the page has an associated master page. If so, the master page merges with the content page before the final Web page is rendered. The page's URL is the address of the content page.

To use a master page, you add a new Master Page item to the project. The page has an extension of .master.

It is possible to nest master pages. Using nested masters, you can define the look for the overall Web site and individual departments or groups can set their own look for their content.

# TIP

To help visualize the size and location of DIV elements, temporarily turn on borders around each element in the element's style and turn them off again when finished.