```
case 5:
    CheckDlgButton(IDC_PENWIDTH5,1);
    break;
default:
    CheckDlgButton(IDC_PENWIDTH0,1);
}
return TRUE;  // return TRUE unless you set the focus to a control
             // EXCEPTION: OCX Property Pages should return FALSE
}
```

You should leave the call to the base class function there because it does some essential setup for the dialog. The switch statement checks one of the radio buttons, depending on the value set in the m_PenWidth data member. This implies that you must arrange to set m_PenWidth to a suitable value before you execute DoModal() because the DoModal() function causes the WM_INITDIALOG message to be sent, resulting in your version of OnInitDialog() called.

The CheckDlgButton() function is inherited indirectly from CWnd through CDialog. If the second argument is 1, it checks the button corresponding to the ID specified in the first argument. If the second argument is 0, the button is unchecked. This works with both checkboxes and radio buttons.

# Handling Radio Button Messages

After the dialog box is displayed, every time you click on one of the radio buttons a message is generated and sent to the application. To deal with these messages, you can add handlers to the CPenDialog class. Right-click each of the radio buttons in turn and select Add Event Handler from the pop-up to create a handler for the BN_CLICKED message. Figure 16-11 shows the event handler dialog window for the button that has IDC_PENWIDTH0 as its ID. Note that I have edited the name of the handler as the default name was a little cumbersome.

![](bbox=[0.176, 0.514, 0.765, 0.82])

Figure 16-11