# How It Works

As soon as you click OK, VS creates a new, empty website for you. This new website contains nothing but a configuration file (called Web.config). In the Solution Explorer, your website now looks like Figure 2-3. If you don't see the top-level Solution node, choose Tools > Options in VS, and in the Projects and Solutions category select Always Show Solution.

![](bbox=[0.68, 0.18, 0.9, 0.33])

Because a website based on the Empty Web Site template is just a simple Windows folder that VS looks at, the actual folder on disk contains the same file. No additional files are used to create the site, as shown in Figure 2-4, which shows File Explorer displaying the files in the folder C:\BegASP.NET\Site.

![](bbox=[0.13, 0.5, 0.88, 0.7])

If you don't see the .config extension of the web file, don't worry. You see how to view file extensions in a later exercise.

As you progress through this book, you'll add new files and folders to the site. These additional files and folders show up in the Solution Explorer and will appear in the Windows folder at C:\BegASP.NET\Site as well.

Opening websites based on the Web Site Project template is very similar to creating new ones. In the next section, you get a quick overview of opening existing sites in VS.

# Opening Existing Websites

Just as with creating new sites, opening an existing site in VS gives you a few options with regard to the source location of the website. You can choose to open a site from the local filesystem, from a local IIS web server, from a remote server using FTP, from a remote site using the Microsoft FrontPage Server Extensions, or from a central Source Control system such as Microsoft's Team Foundation Server. Figure 2-5 shows the Open Web Site dialog box in VS.