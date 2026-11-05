```
private System.Windows.Forms.RadioButton radBtnIntr;
private System.Windows.Forms.RadioButton radBtnFratSor;
private System.Windows.Forms.RadioButton radBtnClub;
private System.Windows.Forms.TextBox txtBxName;
private System.Windows.Forms.TextBox txtBxFund;
private System.ComponentModel.Container components = null;

public PresentationGUI( )
{
    InitializeComponent( );
}
// Windows Forms Designer generated code omitted.

static void Main( )
{
    Application.Run(new PresentationGUI( ));
}

// Objects are instantiated when the form is loaded.
// Another GUI could be designed for entering data.
private void PresentationGUI_Load(object sender,
                                  System.EventArgs e)
{
    aClub = new Club
        ("ACM", "Jones", "Davis 203",
         "Tues", "12:30");
    aFratSorority = new FratSorority
        ("Delta PI", "Brenda Wynn",
         true, "86 SmithField");
    aTeam = new Intramural
        ("Winners", "Joe Kitchen", "VolleyBall");
}

// Three CheckedChanged event-handler methods included.
// Double-clicking on the RadioButton adds the method
// heading and registers the event.
private void radBtnClub_CheckedChanged(object sender,
                                      System.EventArgs e)
{
    this.txtBxName.Text = aClub.OrgName;
    this.aClub.SetFundingAmt( );
    this.txtBxFund.Text = aClub.FundedAmt.ToString("C");
    ShowDetails( );
}
```