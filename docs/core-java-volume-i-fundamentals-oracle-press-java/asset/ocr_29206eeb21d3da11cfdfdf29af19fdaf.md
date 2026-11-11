```
```java
private class ConnectAction implements ActionListener
{
    public void actionPerformed(ActionEvent event)
    {
        // if first time, construct dialog

        if (dialog == null) dialog = new PasswordChooser();

        // set default values
        dialog.setUser(new User("yourname", null));

        // pop up dialog
        if (dialog.showDialog(DataExchangeFrame.this,
"Connect"))
        {
            // if accepted, retrieve user input
            User u = dialog.getUser();
            textArea.append("user name = " + u.getName() + ",
password = "
                    + (new String(u.getPassword())) + "\n");
        }
    }
}
```
```

# Listing 11.14 `dataExchange/PasswordChooser.java`

```
```java
package dataExchange;

import java.awt.BorderLayout;
import java.awt.Component;
import java.awt.Frame;
import java.awt.GridLayout;

import javax.swing.JButton;
import javax.swing.JDialog;
import javax.swing.JLabel;
import javax.swing.JPanel;
```
```