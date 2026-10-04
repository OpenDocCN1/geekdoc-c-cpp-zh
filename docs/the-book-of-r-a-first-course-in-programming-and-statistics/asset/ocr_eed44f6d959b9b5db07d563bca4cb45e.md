# R & Markdown

| Document | Title: rmdown 
|---|---|
| Presentation | Author: |
| Shiny | Default Output Format: |
| From Template | ◉ HTML Recommended format for authoring (you can switch to PDF or Word output). 
| ◯ PDF output requires TeX (MiTeX on Windows, MacTeX 2013+ on OS, R Line 2013+ on Linux).
| ◯ Word Previewing Word documents requires an installation of MS Word (or Libre/OpenOffice on Linux). 
 OK [ Cancel ]

![](bbox=[0.238, 0.273, 0.858, 0.506])

Figure B-10: Starting a new R Markdown file in RStudio. Templates relevant to your chosen output file type are automatically provided.

# Shiny

Shiny is a framework for creating interactive web applications developed by the RStudio. If you're interested in sharing your data, statistical models and analyses, and graphics, you can create a Shiny app. The R package shiny (Chang et al., 2015) provides the required functionality. Shiny apps require you to have an R session running behind the scenes, which is what drives the plots as the user interacts with the application in a web browser.

Like other tools associated with RStudio, Shiny is a high-level framework intended to be friendly for both users and developers. Its emphasis is on creating interactive visuals unlike the graphics produced using ggplot2 in Section 24.4, which you can deploy online for anyone to use.

You can find the Shiny website at http://shiny.rstudio.com/. The development team has a tremendous amount of work into creating comprehensive tutorials, as well as a host of examples. You're comfortable with the app, you can even use Shiny to create interactive documents via R Markdown—notice the Shiny option in the top image of Figure B-10.