button, and then choose Folder and Search Options. Switch to the View tab and deselect the option labeled Hide Extensions for Known File Types. For Windows 8 you find the option called Name Extensions on the View tab of the Ribbon of the File Explorer, as shown in Figure 2-4. You may now need to change the name of the file from styles.txt to styles.css.

When you change the file extension from .txt to .css, Windows may give you a warning that the file becomes unusable if you proceed. You can safely answer Yes to this question to continue.

+   3. Rearrange VS so you can see part of the desktop with the CSS file as well. When you use the Restore Down button next to the Click button on the Windows title bar of VS to get it out of full screen mode.

+   4. Click the CSS file on the desktop and, while holding the mouse button, drag the file into the Solution Explorer and not into other parts of VS, or the file won't added. For example, when you drag it into the Document Window, VS simply opens the file for you, but it doesn't add it.

+   5. When you release the mouse wheel over your website or an existing file in the Solution Explorer, the CSS file is added to your site.

> NOTE If you are using Windows 7 and VS as an administrator, this might not work because Windows doesn't allow the Windows Explorer and VS to communicate. In that case, add existing files using the Add Existing Item menu or use copy and paste.

# How It Works

Although this seems to be a simple exercise that uses basic Windows skills, it serves to show that VS creates a copy of the file when it adds it to the site. The original, styles.css file on the desktop is not affected when you make changes to the copy in VS. This way, it's easy to drag and drop files from existing websites into your new one without affecting the originals. The same applies to files you add using the Adding Item dialog box in VS.

If you have added files to your website's folder outside of VS, they may not show up right away. You can get a fresh copy of the file list by clicking the Refresh button on Solution Explorer's toolbar.

# Organizing Your Site

Because many of the files that make up your site, it's often a good idea to group them by function in separate folders. For example, all style files could go in a folder called Styles, .js files containing JavaScript could in Scripts, user controls could in a Controls folder, and master pages could be stored in a folder called MasterPages. This is a matter of preference, but structured and well-organized sites are easier to manage and understand. The next Try It Out explains how you can move files around into new folders to organize your site.