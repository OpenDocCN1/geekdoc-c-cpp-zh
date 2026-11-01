That's the simple way. The one drawback to this is that there isn't any notification back to the calling code that myForm is finished and has been exited (unless you hook up the Closing or Closed events on the form). Sometimes this isn't a big deal, and the Show method will work fine. If you do need some type of notification, ShowDialog is a better option.

When the Show method is called, the code that follows the Show method is executed immediately. When ShowDialog is called, the calling code is blocked and will wait until the form that ShowDialog called is closed. Not only will the calling code be blocked, but the form will optionally return a DialogResult value. The DialogResult enumeration is a list of identifiers that describe the reason the dialog is closed. These include OK, Cancel, Yes, No, and several others. In order for the form to return a DialogResult, the form's DialogResult property must be set or the DialogResult property on one of the form's buttons must be set.

For example, suppose that part of application asks for the phone number of a client. The form has a text box for the phone number and two buttons; one is labeled OK and the other is labeled Cancel. If you set the DialogResult of the OK button to DialogResult.OK and the DialogResult property on the Cancel button to DialogResult.Cancel, then when either of these buttons is selected, the form becomes invisible and returns to the calling form the appropriate DialogResult value. Now notice that the form is not destroyed; the Visible property is just set to false. That's because you still must get values from the form. For this example, you need to get a phone number. By creating a property on the form for the phone number, the parent form can now get the value and call the Close method on the form. This is what the code for the child form looks like:

```
namespace FormsSample.DialogSample
{
    partial class Phone : Form
    {
        public Phone()
        {
            InitializeComponent();
            btnOK.DialogResult = DialogResult.OK;
            btnCancel.DialogResult = DialogResult.Cancel;
        }

        public string PhoneNumber
        {
            get { return textBox1.Text; }
            set { textBox1.Text = value; }
        }
    }
}
```

The first thing to notice is that there is no code to handle the click events of the buttons. Because the DialogResult property is set for each of the buttons, the form disappears after either the OK or Cancel button is clicked. The only property added is the PhoneNumber property. The following code shows the method in the parent form that calls the Phone dialog:

```
Phone frm = new Phone();
frm.ShowDialog();
if (frm.DialogResult == DialogResult.OK)
{
    label1.Text = "Phone number is " + frm.PhoneNumber;
}
else if (frm.DialogResult == DialogResult.Cancel)
{
    label1.Text = "Form was canceled.";
}
frm.Close();
```

This looks simple enough. Create the new Phone object (frm). When the frm.ShowDialog() method is called, the code in this method will stop and wait for the Phone form to return. You can then check the