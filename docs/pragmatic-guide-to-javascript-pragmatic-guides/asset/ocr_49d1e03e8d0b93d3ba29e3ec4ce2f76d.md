# 26 Using Dynamic Multiple File Uploads

The file upload feature currently built into HTML (as in, pre-HTML5) basically blows. It’s single-file, it has no upload progress feedback, it cannot filter on size or file type constraints, and so on. And it uses Base64 encoding, which means every file sent is blown up by 33 percent. Unless we use stuff like WebSockets or SWFUpload, we are stuck with most of these limitations.

However, we can improve the user experience a bit by letting users pick multiple files in a nice way. When I say “nice” here, I basically mean “without as many visible file controls as there are files.” I like how 37signals presents lists of files-to-be-uploaded in their products: a flat, icon-decorated list of filenames with the option to remove them from the upload “queue.”

![](bbox=[0.12, 0.51, 0.88, 0.65])

The trick is to clone the file field every time its value is set, move the original file field—hidden—in the “queue,” and reset the clone’s value so the field appears blank again. The facing code uses a <ul> for the queue, synthesizing a <li> to hold the file field, filename, and removal icon every time a file is selected. It just feels nicer that way. The next great step would be to exert more control of the input (multiple files at once, size/type constraint enforcement, and so on), but that just isn’t possible with the current <input type="file">; go look up SWFUpload for such nifty features.

The final bit of script shown here gets CSS class names from file extensions using a nice little mapping and handles queue item removal when links in the queue are clicked.