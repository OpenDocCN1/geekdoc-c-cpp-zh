deskt = appsApplications
desktop.hint = desktop
pics.files = pics/*
pics.path = picsexpenses
pics.hint = pics

pkg.name = expenses
pkg.desc = A program to record and SMS expenses
pkg.version = 1.0.0
pkg.domain = window

# ## Figure 24.4. Locating and running the Expenses application

![](bbox=[0.008, 0.295, 0.593, 0.51])

The qtopia_project() line is the same as before. Since this application relies on the Qtopia PIM library, we use a depends() directive to specify the library. If we want to use multiple libraries, we can do so by separating them with commas. The rest of .pro file is similar to what we saw in the Unit Converter example, this time we have a few more source files because the application is more elaborate.

The expenses.desktop file is very similar to the one we saw before:

```
[Desktop Entry]
Comment[]=A program to record and SMS expenses
Exec=expenses/expenses
Icon=expenses/expenses
Type=Application
Name[]=Expenses
```

The same is true of main.cpp:

```
#include <QtopiaApplication>
```