+   5. Above the method, add an enumeration for the days of the week as follows:
enum Day
{
  SUNDAY = 1, MONDAY, TUESDAY, WEDNESDAY,
  THURSDAY, FRIDAY, SATURDAY
}

+   6. Within the method, declare an integer and accept a value from the TextBox, and then declare a string to hold the daily special.
int day = Convert.ToInt32(dayBox.Text);
string special;

+   7. Add a switch structure that lists the daily specials as follows:
switch ((day)
{
  case Day.SUNDAY:
    special = "fried chicken";
    break;
  case Day.MONDAY:
    special = "Sorry - closed";
    break;
  case Day.TUESDAY:
  Day.WEDNESDAY:
  Day.THURSDAY:
    special = "meat loaf";
    break;
  case Day.FRIDAY:
    special = "fish fry";
    break;
  case Day.SATURDAY:
    special = "liver and onions";
    break;
  default:
    special = "Invalid day";
    break;
}

+   8. Following the completed case structure, assign the result to the TextBox property of outputLabel:
outputLabel.Text = "Today's special is " + special;

+   9. Save, compile, and execute the application. The appropriate special is displayed for each day of the week.