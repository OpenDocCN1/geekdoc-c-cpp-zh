Plan the Objects, Properties, and Methods. Plan the objects and property settings for the master page, the seven forms, and their controls.

# The Master Page

| Object | Property | Setting |
|---|---|---|
| Site1.Master | Title | R 'n R |
|  | style(background-color) | Light cyan (or other light color of your choice) |
| Layout | DIV/StyleSheet |  |
| Menu | Items | Home NavigateUrl: Default.aspx |
|  |  | Contact Us NavigateUrl: ContactInformation.aspx |
|  |  | Underline: |
|  | Font |  |
| LoginStatus | LogoutPageUrl | LoggedOut |
|  | Layout Action | Redirect |
|  | Font | Underline: |
| Header | Image1 | ImageUrl: BlueHills.jpg |
|  | Image2 | R'nRHeading.gif (Add the files from the StudentData folder to the project's Images folder before setting the property.) |
| ContentPlaceHolder | Name | ContentPlaceHolder1 |
| Footer | Text | Copyright 2009 R 'n R — For Reading and Refreshment |