
| CONTROL | DESCRIPTION |
| :--- | :--- |
| DropShadowExtender | This extender applies a drop shadow to an ASP.NET Panel control. The extender allows you to specify how wide the shadow is, how opaque it is, and whether the shadow should have rounded corners. For pages that let the user move or resize the panel, the DropShadowExtender has a mode that will resize and reposition the shadow to match the target panel at run-time. |
| DynamicPopulateExtender | This extender replaces the contents of a control with the result of a web service or page method call. The method call returns a string of HTML that is inserted as a child of the target element. |
| FilteredExtender | This is an extender that lets users enter only characters that you define into a text box or prevents users from entering characters that you specify. |
| HoverMenuExtender | This is an extender that can be attached to any .NET WebControl, and will associate that control with a pop-up panel to display additional content. When the user moves the cursor over the main control, two things happen. The pop-up panel is displayed at a position specified by the page developer (at the left, right, top, or bottom of the main control). Optionally, a CSS style is applied to the control to specify it as "hot". |
| Editor | This control allows you to easily create and edit HTML content. Various buttons in the toolbar are used for content editing. You can see generated HTML markup and a preview document. |
| ListSearchExtender | This extender selects items in a ListBox or DropDownList by typing. The extender performs an incremental search within the ListBox based on what has been typed so far. The prompt message that is displayed when you click the list can be customized, along with its CSS class and position. |

## TABLE 20-1 (continued)

| CONTROL | DESCRIPTION |
| :--- | :--- |
| MaskedEditExtender | This extender attaches to a TextBox control to restrict the kind of text that can be entered. MaskedEditExtender applies a "mask" to the input that permits only certain types of characters to be entered. The supported data formats are Number, Date, Time, and DateTime. MaskedEditExtender uses the culture settings specified in the CultureName. If not specified, the culture setting will be the same as the page. |
| ModalPopupExtender | This extender allows you to display content in elements that mimic a dialog box, which prevents the user from interacting with the rest of the page. The modal content can contain any hierarchy of controls. It is displayed above a background (in z-order) that can have a custom style applied to it. |
| MultiHandleSliderExtender | This extender provides a feature-rich extension to a regular TextBox control. It allows you to choose a single value, or multiple values in a range, through a graphical slider interface. It supports one handle, or any number of handles bound to the values of TextBox or Label controls. It also provides options for read-only access, custom styling, and drag handles, as well as mouse and keyboard support for accessibility. |
| MutuallyExclusiveExtender | This extender can be attached to any CheckBox control. By adding a number of checkboxes to the same "Key," only one checkbox with the specified key can be checked at a time. This extender is useful when a number of choices are available, but only one can be chosen (similar to a radio button). The use of checkboxes, however, allows you to uncheck a value, which is normally not possible with radio buttons. This also provides a more consistent and expected interface than using JavaScript to allow the de-selection of a RadioButton item. |

| CONTROL | DESCRIPTION |
| :--- | :--- |
| NoBot | This control attempts to provide CAPTCHA-like bot/spam prevention without requiring any user interaction. This approach is easier to bypass than an implementation that requires actual human intervention, but NoBot has the benefit of being completely invisible. NoBot is probably most relevant for low-traffic sites where blog spam is a problem and 100 percent effectiveness is not required. |
| NumericUpDownExtender | This is an extender that can be attached to a TextBox control to add "up" and "down" buttons that increment and decrement the value in the TextBox. The increment and decrement can be simple +/-1 arithmetic. They can cycle through a provided list of values (like the months of the year), or they can call a web service to determine the next value. Page authors can also provide custom images to be used instead of the default up/down buttons. |
| PagingBulletedListExtender | This extender can be attached to a BulletedList. The extender provides paging for the bulleted list. You can customize the number of items displayed per page and the appearance of the page-navigation controls. |
| PasswordStrength | This is an extender that can be attached to a TextBox to show the strength of the password as the user types. It provides a visual indicator of how strong the password is. |
| PopupControlExtender | This extender allows you to display a pop-up window over a control. The pop-up can contain any hierarchy of controls and can be positioned relative to the target control. It is triggered by various events or programmatically. |

## TABLE 20-1 (continued)

| CONTROL | DESCRIPTION |
| :--- | :--- |
| Rating | This control allows users to rate items using a set of stars. You can customize the number of stars, the range, and the appearance of the stars. |
| ReorderList | This control allows users to reorder items in a list by dragging and dropping them. It provides an intuitive way to manage list order. |
| ResizableControlExtender | This is an extender that can be attached to any control to make it resizable. It provides a handle that the user can drag to change the width and height of the target control. |
| RoundedCornersExtender | This extender applies rounded corners to a control. You can specify the radius of the corners and the color of the border. |
| SeaDragon | This control allows users to pan and zoom around an image. It provides controls for navigating high-resolution images. |
| SliderExtender | This is an extender that can be attached to a TextBox to allow the user to choose a value from a range. The slider can be horizontal or vertical and can also act as a discrete slider. |

| CONTROL | DESCRIPTION |
| :--- | :--- |
| SlideShowExtender | This is an extender that targets image controls. You can provide it with buttons to Previous, Next, and Play. You can configure the slide show to play automatically on render, allow it to loop through the images, and also set the interval for slide transitions. You can use a page method to supply images to the slide show. |
| TabContainer | This is a control that creates a set of tabs that can be used to organize page content. A TabContainer is a host for a number TabPanel controls. |
| TextBoxWatermarkExtender | This extender can be attached to a TextBox to get watermark behavior. When a watermarked TextBox is empty, it displays a message to the user with a custom CSS style. Once the user has typed text into the TextBox, the appearance goes away. The typical purpose of a watermark is to provide more information to the user about the TextBox itself without cluttering the rest of the page. |
| ToggleButtonExtender | This extender can be attached to a CheckBox control. ToggleButtonExtender enables the use of custom images to show the state of the CheckBox. The behavior of the CheckBox is unaffected. |
| UpdatePanelAnimationExtender | This is a simple extender that allows you to utilize the powerful animation framework with existing pages in easy, decorative fashion. It is used to play animations while an UpdatePanel is updating, and after it has finished updating. |
| ValidationCalloutExtender | This extender enhances the functionality of existing ASP.NET validators. To use this, add an input field and a validator control as you normally would, and attach a ValidationCalloutExtender to it. |

# New Server Controls

The AjaxControlToolkit.dll adds several ASP.NET controls to the Toolbox. Most of them are very simple and intuitive to use. However, they have many properties and methods you can use.
