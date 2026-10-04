
```
R> getOption("repos") CRAN
"http://cran.stat.auckland.ac.nz"
```

To change this is to say, the mirror at the University of Melbourne, simply assign the new URL to the repos component in a call to options as follows:

```
R> options(repos="http://cran.ms.unimelb.edu.au/")
```

Any subsequent use of install.packages or update.packages will now use this Australian mirror for downloads.

### A.4.2 Other Package Repositories

CRAN isn't the only repository of R packages. Other repositories include Bioconductor (see https://www.bioconductor.org/), Omegath (see http://www.omegath.org/), and R-Forge (see https://r-forge.r.project/), and there are several. These repositories tend to deal with different subjects. Bioconductor, for example, hosts packages that deal with DNA microarray and other genomic analysis methodologies; Omegath hosts packages that focus on web and Java-based applications.

In terms of general statistics, CRAN is the go-to repository for most users. To learn more about the other repositories, you can visit the associated websites.

### A.5 Citing and Writing Packages

It's important that the work put into R and its packages is recognized in the appropriate way when the software is used in, for example, data analysis as part of your research projects. Indeed, when you get to the stage where you're thinking about writing your own packages, it pays to be aware of the following.

#### A.5.1 Citing R and Cont Packages

For citing R and/or its packages, the citation command produces the relevant output.

```
R> citation()
```

To cite R in publications use:

- R Core Team (2016). A language and environment for statistical computing.
- R Foundation for Statistical Computing, Vienna, Austria. URL https://www.R-project.org/

- A BibTeX entry for LaTeX users is

```
@Manual{
  title = {R: A Language and Environment for Statistical Computing},
  author = {{R Core Team}},
  organization = {R Foundation for Statistical Computing},
  address = {Vienna, Austria},
  year = {2016},
  url = {https://www.R-project.org/},
}
```

We have invested a lot of time and effort in creating R, please cite it using it for data analysis. See also 'citation("pkgname")' for citing R packages.

Note that LaTeX users are conveniently catered to via automatically generated BibTeX entries.

You can cite individual packages if these have been instrumental in completing a particular piece of work. Here's one example:

```
R citation("MASS")
```

To cite the MASS package in publications use:

Venables, W. N. & Ripley, B. D. (2002) Modern Applied Statistics with S. Fourth Edition. Springer, New York. ISBN 0-387-95457-0

A BibTeX entry for LaTeX users is

```
@Book(
  title = {Modern Applied Statistics with S},
  author = {W. N. Venables and B. D. Ripley},
  publisher = {Springer},
  edition = {Fourth},
  address = {New York},
  year = {2002},
  note = {ISBN 0-387-95457-0},
  url = {http://www.stats.ox.ac.uk/pub/MASS4},
)
```

### A.5.2 Writing Your Own Packages

Once you become an R expert, you may find yourself with a suite of functions, data sets, and objects that others might find useful or that enough to warrant packaging them in a standardized, easily loadable format. There's certainly no obligation to submit your packages to CRAN or any other repository, but if you do aim to do so, note that there rather strict requirements to assure users of the stability and compatibility of your package.

If you're interested in constructing your own installable R package, see the official Writing R Extensions manual, accessible on any CRAN mirror site by clicking the Manuals link under Documentation on the left of the home page; you can see this link in Figure A-2. If you're interested, you may also want to seek out the book by Wickham (2015b), which provides useful instruction on the R package-writing process and associated dos and don'ts.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_784_0.png)

# WORKING WITH RSTUDIO

Although the base R application and GUI are all you need to unleash the full suite of available functionality, the bare-bones appearance of the console and code editor can be off-putting to some, especially beginners. One of the best integrated development environments (IDEs) designed specifically to enhance day-to-day use of the R language is RStudio.

Like R, the desktop version of RStudio (RStudio Team, 2015) is free and can be used on Windows, OS X, and Linux systems. Before installing RStudio, you must first have R installed, as described in Appendix A (OS X users will also need XQuartz, see Section A.1). Then, you can download RStudio from the official website at https://www.rstudio.com/products/rstudio/download/

The R RStudio website also hosts a variety of support articles and links, as well as instructions for various special enhancements, of which are noted in Section B.2. If you need help with RStudio, see https://support.rstudio.com/hc/en-us/. In particular, you should take time to click the Documentation link; you can also view this through RStudio by selecting Help → RStudio Docs.

In this appendix, you'll get an overview of RStudio and its most commonly used tools.

### B.1 Basic Layout IDE

The RStudio is split into four panes, and you can customize the content and layout to suit your preferences. Figure B-1 shows my setup. In it, I'm playing with the ggvis code from Section 24.4.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_785_0.png)

> Figure B-1: RStudio in action. The four panes can be arranged and suppressed as you like; here, you can see the code editor (top left), the console (bottom left), the help pages (top right), and the graphics viewer (bottom right). The panes on the right also have tabs to choose from.

You write R code in the built-in editor and execute it in the console: the shortcut 'send to console' keystrokes are CTRL-ENTER or CTRL-R in Windows and ⌘-RETURN on a Mac. The textual output appears in the console as usual.

### B.1.1 Editor Features and Appearance Options

One of the most useful features of RStudio editor is the color-themed highlighting and bracket matching. This makes for an easier coding experience than the base R editor, particularly when writing long chunks of code. There are also autocomplete options that pop up as you're typing in either the editor or the console. You can see an example of this in Figure B-2.

752 Appendix B

| | |
| :--- | :--- |
| input_checkbox (gvis) | input_radiobootsa(choices, selected = NULL, label = '', id = rand_id('radio'), map = identity) |
| input_checkboxgroup (gvis) | * input_radiobootsa only selects one value |
| input_numeric (gvis) | * input_checkboxgroup can always select multiple values |
| input_robuttons (gvis) | * input_select can select one value; otherwise the user can select multiple using modifier keys |
| input_select (gvis) | Press F1 for additional help |
| input_slider (gvis) | |
| input_text (gvis) | |

Figure B-2: RStudio's autocomplete feature includes hints about each option.

| General | Editing | Completion | Diagnostics | |
| :--- | :--- | :--- | :--- | :--- |
| General | Insert space for tab | | | Editor font: Menlo | plotting of objects |
| Editing | Insert matching brackets/quotes | | | Font size: 11 | function(x, y, ...) { |
| Completion | Auto-indent code after | | | | plot(multi(strategy, "class")) |
| Diagnostics | select all on auto-indent | | | Editor Theme: Dark | if (is.character(x)) { |
| Appearance | Soft-wrap code lines | | | View Files | function(x, y, ...) = ... {
| Appearance | Show invisible characters | | | File Search | match(character(x), ...)) |
| Appearance | Show line numbers at right margin | | | File Markers | |
| Appearance | Strip horizontal whitespace when inserting | | | Pattern on Dawn | |
| Appearance | Continue comment when inserting new line | | | Theme: Night Bright | |
| Appearance | Enable editing mode | | | Theme: Light | |
| Execution | Always ask R scripts before running | | | Twilight | |
| Execution | Prevent undo/redo after executing from source | | | Splitting | |
| Snippets | Enable code snippets [x] | | | Cursor | |
| Publishing | | | | Publishing | |

Figure B-3: The options for code editing (left) and appearance (right)

### B.1.2 Customizing Panes

Next you will probably want to sort the arrangement and content of the four RStudio panes. Two panes will always be the editor and the console, but you can set up an additional number of tabs to be displayed on the utility panes. These include a file browser you can use to search for and open R scripts on your local machine, plot and document viewers, R function help, and a package installer.

You can configure your utility panes with checkboxes in the Pane Layout of the RStudio options. Figure B-4 shows my current settings; one change I made from the default arrangement is to make help files appear in the topmost pane, with the graphical displays at the bottom, since I want to refer to function documentation while experimenting with my plots.
