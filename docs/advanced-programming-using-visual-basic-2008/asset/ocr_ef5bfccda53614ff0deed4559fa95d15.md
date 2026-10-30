# Case Studies

# Claytor's Cottages

Modify the Reservations option of the Claytor's Cottages case study project from Chapter 2 to use a WCF Service for the calculations.

> Note: If you prefer, use a calendar control, in which case you do not need the text box for number of nights or the check boxes for weekend/weekday.

# Presentation Tier

The form should have a drop-down list or radio buttons for King, Queen, or Double. Include text boxes for entering the customer's name, phone number, the number of nights stayed, credit card type (use a combo box for Visa, Mastercard, and American Express), and credit card number. Name, nights stayed, and credit card number are required fields. Use a check box for weekend or weekday rate and a check box for AARP or AAA members. Display the price on the form.

# WCF Service Tier

Calculate the price using the following table, which also appears in the Chapter 2 case study. Add a room tax of 7 percent. AAA and AARP customers receive a 10 percent discount rate.

| Beds | Sunday through Thursday rate | Weekend rate (Friday and Saturday) |
| King | 95.00 | 105.00 |
| Queen | 85.00 | 95.00 |
| Double | 69.95 | 79.95 |

# Christian's Car Rentals

Modify your Christian's Car Rentals project from Chapter 2. Code the Rentals form using a WCF Service for the calculations.

Make sure that an entry has been made for driver's license and that the number of days rented is greater than 0.

# Presentation Tier

The presentation tier should include data entry for the size of car: Economy, Mid size, or Luxury. Include text boxes for entering the renter's name, phone number, driver's license, credit card type, and credit card number. Use a combo box to select the credit card type. A group box should include the number of days rented, the beginning odometer reading, and the ending odometer reading.

Validate that the ending odometer reading is greater than the beginning odometer reading before allowing the data to be sent to the service component.

# WCF Service

There is no mileage charge if the number of miles does not exceed an average of 100 miles per day rented. Use the following rate table, which also appears in the Chapter 2 case study.

| Car size | Daily rate | Mileage rate |
| Compact | 26.95 | .12 |
| Mid size | 32.95 | .15 |
| Luxury | 50.95 | .20 |