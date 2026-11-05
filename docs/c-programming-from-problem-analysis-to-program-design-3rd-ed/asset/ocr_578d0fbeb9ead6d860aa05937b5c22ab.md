```
#region Windows Form Designer generated code
    // Required method for Designer support - do not modify
    // the contents of this method with the Code Editor.
    private void InitializeComponent( )
    {
        this.SuspendLayout( );
        // Form1
        this.AutoScaleDimensions = new System.Drawing.SizeF(10F,
            19F);
        this.AutoScaleMode = System.Windows.Forms.AutoScaleMode.
            Font;
        this.AutoScroll = true;
        this.BackColor =
            System.Drawing.Color.FromArgb(((System.Byte)(255)),
            ((System.Byte)(224)), ((System.Byte)(192)));
        this.ClientSize = new System.Drawing.Size(392, 373);
        this.Font = new System.Drawing.Font("Arial", 12F,
            System.Drawing.FontStyle.Bold,
            System.Drawing.GraphicsUnit.Point,
            ((System.Byte)(0)));
        this.ForeColor = System.Drawing.Color.Blue;
        this.Location = new System.Drawing.Point(30, 30);
        this.Margin = new System.Windows.Forms.Padding(4, 4, 4,
            4);
        this.MaximizeBox = false;
        this.Name = "Form1";
        this.StartPosition =
            System.Windows.Forms.FormStartPosition.CenterScreen;
        this.Text = "First Windows Application";
        this.FormClosing +=
            new System.Windows.Forms.FormClosingEventHandler
            (this.Form1_FormClosing);
        this.ResumeLayout(false);
    }
}
#endregion
}
// End of Form1.Designer.cs  file
```

```
// Program.cs
using System;
using System.Collections.Generic;
using System.Windows.Forms;

namespace FirstWindows
{
    static class Program
    {
```