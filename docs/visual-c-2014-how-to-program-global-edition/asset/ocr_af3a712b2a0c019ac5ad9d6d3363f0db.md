# 17.5 Case Study: Credit-Inquiry Program 755

```
// Fig. 17.7: CreditInquiryForm.cs
// Read a file sequentially and display contents based on
// account type specified by user (credit, debit or zero balances)
using System;
using System.Windows.Forms;
using System.IO;
using BankLibrary;

namespace CreditInquiry
{
    public partial class CreditInquiryForm : Form
    {
        private FileStream input; // maintains the connection to the file
        private StreamReader FileReader; // reads data from text file

        // parameterless constructor
        public CreditInquiry()
        {
            InitializeComponent();
        }

        // invoked when user clicks Open button
        private void onClick_Click(object sender, EventArgs e)
        {
            // create dialog box enabling user to open file
            DialogResult result;
            string fileName;

            using (OpenFileDialog chooser = new OpenFileDialog())
            {
                result = chooser.ShowDialog();
                fileName = chooser.FileName;
            }

            // exit event handler if user clicked Cancel
            if (result == DialogResult.OK)
            {
                // show error if user specified invalid file
                if (string.IsNullOrEmpty(fileName))
                {
                    MessageBox.Show("Invalid File Name", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
                else
                {
                    // create FileStream to obtain read access to file
                    input = new FileStream(fileName, FileMode.Open, FileAccess.Read);
                    FileReader = new StreamReader(input);
                }
                // set file from where data is read
                FileReader = new StreamReader(input);
            }
        }
    }
```

Fig. 17.7 | Credit-inquiry program. (Part I of S.)