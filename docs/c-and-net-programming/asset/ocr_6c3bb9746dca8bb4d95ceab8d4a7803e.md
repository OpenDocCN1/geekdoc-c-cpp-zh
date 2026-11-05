```
~~~csharp
            flowPanel.Dock = DockStyle.Fill;
            flowPanel.BorderStyle = BorderStyle.FixedSingle;

            var button = new Button();
            button.Margin = new Padding(10, 10, 0, 0);

            button.Text = "Quit";
            button.AutoSize = true;
            button.Click += new EventHandler(OnClick);

            flowPanel.Controls.Add(button);
            Controls.Add(flowPanel);

            CenterToScreen();
        }

        void OnClick(object sender, EventArgs e)
        {
            Close();
        }

        [STAThread]
        static void Main()
        {
            Application.SetHighDpiMode(HighDpiMode.SystemAware);
            Application.EnableVisualStyles();
            Application.Run(new MyForm());
        }
    }
}
~~~
```

Q.10 Develop a C# windows forms application for students enrollment in Inter-College Technical Contest, with appropriate from events, controls, menus and dialog boxes. (Refer section 20.5)
AU : May-18, Marks 15

Q.11 Write a C# Program to Perform Addition with MOUSEUP Event.
AU : Dec.-18, Marks 16

Ans. :

```
~~~csharp
/*
 * C# Program to Perform Addition with MOUSEUP Event
 */
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
~~~
```