The lines appear on the form the layouts that have been created, as shown in Figure 2.8. They don't appear when the form is run.

# ### Figure 2.8. The form with the layouts

![](bbox=[0.009, 0.096, 0.296, 0.196])

Now click Edit Tab Order. A number in a blue rectangle will appear next to every widget that can accept focus, as shown in Figure 2.9. Each widget in turn in the order you want them to accept focus, then click Edit Widgets to leave tab order mode.

# ### Figure 2.9. Setting the form's tab order

![](bbox=[0.009, 0.384, 0.296, 0.484])

To preview the dialog, click the Form Preview menu option. Check the tab order by pressing Tab repeatedly. Close the dialog using the close button in the title bar.

Save the dialog as gotocelldialog.ui in a directory called gotocell, and create a main.cpp in the same directory using a plain text editor:

```
#include <QApplication>
#include <QDialog>

#include "ui_gotocelldialog.h"

int main(int argc, char argv[])
{
    QApplication app(argc, argv);

    Ui::GotoCell ui;
    QDialog dialog = new QDialog;
    ui.setupUi(dialog);
    dialog->show();

    return app.exec();
}
```