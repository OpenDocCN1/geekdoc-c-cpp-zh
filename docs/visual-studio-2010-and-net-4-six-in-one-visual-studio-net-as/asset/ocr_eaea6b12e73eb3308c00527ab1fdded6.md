# Metadata Attributes

In cases, it may be necessary to associate information with proffered or consumed services. Often, the information is used to explain the capabilities of a specific implementation of a common contract. Also, this information can be used to determine which implementation of a contract should be used during the composition phase.

Let's assume that you provided more than one service for the earlier IContextInfo contract. How can the MEF decide which one should be used? If you do not support some other information helping the MEF in decision, it will not do the match-matching between IContextInfo services and consumers.

The MEF allows attaching metadata attributes to services and consumers — owners of Export and Import attributes. The Visual Studio editor uses these attributes heavily for many purposes, including the following:

+   - Providing information that is displayed in the IDE editor extension (for example, in the Fonts and Colors dialog)

+   - Determining the order in which competing components (that is, components implementing the same contract)

+   - Where user interface elements custom margins should be placed in the IDE

+   - Assigning information to the components in order to provide a way to reference them from other components

Just as for Export and Import attributes, you will see concrete metadata attributes in the custom editor classifier sample later in this chapter.

# Editor Extensibility Points

The Visual Studio 2010 editor provides a dozen extensibility points where developers can add their own components to change or extend the default behavior. Although this book does not examine editor extensions in detail, Table 6-8 lists the major extensibility points to help you imagine what sorts of options you have when thinking about the default behavior of the code editor.

TABLE 6-8: Major Editor Extensibility Points

| EXTENSIBILITY POINT | DESCRIPTION |
| --- | --- |
| Content type definition | The text behind the code editor is always associated with a content type. The content type determines how specific text should be handled in the editor. For example, different syntax coloring should be used for texts having "CSharp" content type than the "Basic." Most editor extensions are associated with a content type to define where to use them. Content types form a hierarchy having the "text" type as root. Content type extensibility allows developers to define their own content types, and put it into this hierarchy.