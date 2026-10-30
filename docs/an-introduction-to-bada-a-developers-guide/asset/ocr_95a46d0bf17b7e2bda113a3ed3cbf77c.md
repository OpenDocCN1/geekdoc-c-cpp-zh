One aspect of localisation is ensuring that all the text you display in your application’s UI matches the user’s language settings.
Another is ensuring that everything you display to the user is in a format that they expect. Date and time information should appear in the right format for a particular country and language setting, with the appropriate separators, and day and month names. Numbers should appear with the correct separators and the appropriate currency symbols should be used. In bada, support for localised number formats, dates, times, and currency is provided by the classes in the Locales namespace. (More on this in Chapter 6).
Supporting multiple languages and date, time, and number formats really improves your application’s chances of worldwide success. The rest of this section will show you how to build multilingual support into your UI. Fortunately, bada makes this easy. Everything you need to create a multilingual UI is included in the UI Builder.

# 2.6.1 Add New Languages

Adding languages is easy. To support additional languages, open the Resource Explorer in the IDE. Double click String. Right-click inside the String window and from the menu displayed, choose Language Setting. The Add New Language dialogue is now displayed, as shown in Figure 2.19.

![](bbox=[0.15, 0.64, 0.75, 0.92])

Figure 2.19 Adding a new language in the UI Builder string table view.