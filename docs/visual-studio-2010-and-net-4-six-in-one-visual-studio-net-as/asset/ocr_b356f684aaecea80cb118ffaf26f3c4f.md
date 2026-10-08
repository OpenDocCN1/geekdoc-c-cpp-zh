```
PromptText="Please select an Expert"
LoadingText="Loading..."
ServicePath="ExpertiseService.asmx"
ServiceMethod="GetDropDownContent" />
</form>
```

As you can see since, there are many properties used by CascadingDropDown. TargetControlID tells the extender which PromptText tells what to use for the default item in the list representing that no item is selected. When the control's content is loaded, the text defined by LoadingText is displayed in the control.

The content of the DropDownList may have different content depending on the UI logic. For example, at benefiting a use case, it may contain vehicle categories, or later concrete car models. The category is the only content of the DropDownList should be populated.

The second extender with the codExtender identifies a property name ParentControlID. It represents the identifier of the DropList that is used as the parent control. As the parent's values change, it is re-populated according to the value selected in the parent control. For example, in the FindExpertDemo, when the user uses the Expertise drop-down to "Visual Basic," the Expert drop-down is populated with the name of Visual Basic experts.

The CascadingDropDown extender uses ASP.NET web services to populate the content of the attached DropDownList. The ServicePath property refers to the web service responsible for the population, while ServiceMethod handles the name of the method to be called. This method has the following signature:

```
public CascadingDropDownValue[] ServiceMethodName(string knownCategoryValues,
  string category);
```

The knownCategoryValues argument contains entries when the service is called for a DropDownList that is not parent (ParentControlID is set), or by the parent control's Category property and its selected. The category argument is for the control's Category property. For example, when the ExpertiseList is populated, knownCategoryValues is an empty string, while category is set to "Expertise." When you select "Visual Basic" the service is called to populate the ExpertiseList control with knownCategoryValues set to Expertise;1 and category to Expert.

# Adding the ExpertiseService Class to the Project

So, in order to populate the lists, add a new web service item to the project and name it Expertise. Listing 20-4 shows the code you should copy into this new web service file.

LISTING 20-4: ExpertiseService.asmx.cs

```
using System;
using System.Collections.Generic;
using System.Collections.Specialized;
using System.Web.Services;
```