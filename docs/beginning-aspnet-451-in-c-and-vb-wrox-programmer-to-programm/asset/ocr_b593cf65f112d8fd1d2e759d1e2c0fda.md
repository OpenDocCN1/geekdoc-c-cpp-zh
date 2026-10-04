# 19
Deploying Your Website

WHAT YOU WILL LEARN IN THIS CHAPTER:

+   * How to ease the deployment process through simple changes to your code and configuration
* How to publish your site from Visual Studio
* How to install and configure a web server that is ready for release into the wild on your target machine
* How to avoid common errors you may get when deploying a site
* How to copy data stored in your SQL Server database to the target server

WROX.COM CODE DOWNLOADS FOR THIS CHAPTER

You can find the wrox.com code downloads for this chapter on the Download Code tab at www.wrox.com/begaspnet451. The code is in the Chapter 19 folder.

Congratulations! The fact that you're reading this chapter probably means you now have a full-featured, database-driven ASP.NET website that is ready for release into the wild. It's an exciting time for you and your project. Pretty soon your application will be used and judged by your target audience.

To make your website accessible to users worldwide, you need to publish it to a production server that is connected to the Internet. What kind of server is this and where is it located depends on your own requirements and budget. You can host the site on a home server in your attic with a private Internet connection (as I used to do with http://imar.spananjaars.com) or you can host it with an external (and often commercial) party with a direct connection to the Internet backbone.

Either way, you will need to do some work to get your site from its development location at C:\BegASPNET\Site to a location where it's accessible over the Internet.