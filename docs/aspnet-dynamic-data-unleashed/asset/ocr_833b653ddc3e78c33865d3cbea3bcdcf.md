You can use any of the built-in or third-party ASP.NET controls to implement user interface appropriate for entering search values for a data type the template is designed to handle. This template is designed for String columns. It uses a TextBox control similar to the one used in the sample search page earlier. The OnTextChanged event handler is used to refresh the query results when the user changes the search value.

# LISTING 5.4  Text Filter Template (Code-Behind)

```
using System;
using System.Linq;
using System.Linq.Dynamic;
using System.Web.DynamicData;
using System.Web.UI;

namespace WebApplication.DynamicData.Filters
{
    public partial class TextFilter : QueryableFilterUserControl
    {
        public override IQueryable GetQueryable(IQueryable query)
        {
            if (!string.IsNullOrEmpty(this.textBox.Text))
            {
                string filter = this.Column.Name + " == @0";
                query = query.Where (filter, this.textBox.Text);
            }

            return query;
        }

        protected override void OnInit(EventArgs e)
        {
            base.OnInit(e);
            this.textBox.MaxLength = this.Column.MaxLength;
            this.textBox.Text = this.DefaultValue;
        }

        protected void TextBox_TextChanged(object sender, EventArgs e)
        {
            this.OnFilterChanged();
        }
    }
}
```