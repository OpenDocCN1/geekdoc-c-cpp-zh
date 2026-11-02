Note that the control definition code must be executed before WinJS.UI.process/processAll so that the constructor function named in data-win-control actually exists at that point.

For a more complete control, you can take a look at the HTML SemanticZoom for custom controls. sample. There is also a post on the Windows Developer blog that takes a patterns-oriented approach to this subject. As for us here, let's work with the CalendarControl example in this chapter's companion content, which was created by my friend Kenichiro Tanaka of Microsoft Tokyo and is shown in Figure 5-9. (Note that this is example is only partly sensitive to localized calendar settings; it is not meant to be full-featured.)

Following the steps given earlier, this control is defined using WinJS.Class.define within a Controls namespace (controls/calendar/calendar.js lines 4-12 shown here):

```
WinJS.Namespace.define("Controls", {
  Calendar : WinJS.Class.define(
    // constructor
    function (element, options) {
      this.element = element || document.createElement("div");
      this.element.className = "control-calendar";
      this.element.winControl = this;
```

The rest of the constructor (lines 14-72) builds up the child elements that define the control, making sure that each piece has a particular class name that, when scoped with the control-calendar class placed on the root element above, allows specific styling of the individual parts. The defaults for this are in controls/calendar/calendar.css; specific overrides that differentiate the two controls in Figure 5-9 are in css/default.css.

![](bbox=[0.18, 0.72, 0.88, 0.92])

FIGURE 5-9 Output of the Calendar Control example.