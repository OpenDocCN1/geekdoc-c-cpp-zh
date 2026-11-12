+   - genstrings

This command-line utility can parse C and Objective-C files and can find all the keys declared using one of the NSLocalizedString() methods. It will then build the .strings files containing all the unique values it found. This file can then be sent to translators, and the translated versions can be placed in the appropriate language bundles.

Additionally, we don’t need to translate every single string in our application. We only need to localize the strings that the user actually sees. Strings used as internal keys or as the names of notifications should be left alone.

For more information, see the Internationalization Programming Topics.

# # ACCESSIBILITY

Recently, iOS has received a lot of praise and press for its excellent accessibility features. Out of the box, iOS provides a wide range of alternate input and output settings to assist people with low vision or blindness, hearing disabilities, and motor or physical disabilities. For the most part, these features are available to our application for free. We may need to be a little careful when creating custom gestures, since assistive touch won’t support them, but other than that, we can focus all our attention on supporting VoiceOver.

For most standard controls, we just need to set the Accessibility settings in Interface Builder. These can be found in the Identity inspector. The label is a string that succinctly identifies the control. For example, “Units” or “Enter Weight.”

The hint is a brief string that describes the effect of performing an action on the control. This should avoid mentioning either the control or the action. For example, “enter a new weight” not “select this text field to enter a new weight.”

This, however, is just the beginning. iOS accessibility support provides a number of methods to help truly customize and refine the interface. I highly recommend reading through the Accessibility Programming Guide for iOS for more information.