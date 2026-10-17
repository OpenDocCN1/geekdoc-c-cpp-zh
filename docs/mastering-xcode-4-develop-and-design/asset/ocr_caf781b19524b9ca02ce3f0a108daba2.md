Although only the Product Name field is required, you should always provide a suitable company identifier. The identifier doesn’t necessarily have to correspond to an existing domain, but it should be unique.

The App Store Category pop-up lets you select a general category under which your application would fall if you choose to deploy to the Mac App Store. Since you won’t be submitting TestApp to the App Store, you can leave that set to None, its default.

The next three options (Create Document-Based Application, Document Class, and Document Extension) let you use a document-based application template. A plain Cocoa application (Create Document-Based Application deselected) is intended for applications that do not work with individual files as documents; a document-based Cocoa application uses the Cocoa document architecture to open and manipulate document files. For simplicity, TestApp will not be document-based, so leave that option deselected.

The Use Core Data option adds support for Cocoa’s object graph management and persistence framework, called Core Data. Select this option so you can explore the Data Model Editor in Chapter 10.

The Include Unit Tests option will add support for unit tests to your project. Select this option to include unit tests, which you’ll explore in Chapter 18.

The Include Spotlight Importer option adds a Spotlight importer plug-in as a dependent build target to your project’s application target. When you add the necessary code, Spotlight—the Mac OS X search facility—will use the importer to add the data you provide to its search index automatically. Leave this deselected, and leave Spotlight importer plug-in programming for another book.

Different project and option choices can cause different fields to appear when creating a new project. Consult the Xcode documentation (covered in Chapter 4) for further details about these options.