
## Listing 7.5 (Continued)

```java
/**
 * Sets the current locale.
 * @param locale the desired locale
 */
public void setCurrentLocale(Locale locale)
{
    currentLocale = locale;
    localeCombo.setLocale(currentLocale);
    localeCombo.setSelectedItem(currentLocale);

    res = ResourceBundle.getBundle("retire.RetireResources", currentLocale);
    resStrings = ResourceBundle.getBundle("retire.RetireStrings", currentLocale);
    currencyFmt = NumberFormat.getCurrencyInstance(currentLocale);
    numberFmt = NumberFormat.getNumberInstance(currentLocale);
    percentFmt = NumberFormat.getPercentInstance(currentLocale);

    updateDisplay();
    updateInfo();
    updateData();
    updateGraph();
}

/**
 * Updates all labels in the display.
 */
public void updateDisplay()
{
    languageLabel.setText(resStrings.getString("language"));
    savingsLabel.setText(resStrings.getString("savings"));
    contribLabel.setText(resStrings.getString("contrib"));
    incomeLabel.setText(resStrings.getString("income"));
    currentAgeLabel.setText(resStrings.getString("currentAge"));
    retireAgeLabel.setText(resStrings.getString("retireAge"));
    deathAgeLabel.setText(resStrings.getString("deathAge"));
    inflationPercentLabel.setText(resStrings.getString("inflationPercent"));
    investPercentLabel.setText(resStrings.getString("investPercent"));
    computeButton.setText(resStrings.getString("computeButton"));
}

/**
 * Updates the information in the text fields.
 */
public void updateInfo()
{
    savingsField.setText(currencyFmt.format(info.getSavings()));
    contribField.setText(currencyFmt.format(info.getContrib()));
    incomeField.setText(currencyFmt.format(info.getIncome()));
    currentAgeField.setText(numberFmt.format(info.getCurrentAge()));
    retireAgeField.setText(numberFmt.format(info.getRetireAge()));
    deathAgeField.setText(numberFmt.format(info.getDeathAge()));
    investPercentField.setText(percentFmt.format(info.getInvestPercent()));
    inflationPercentField.setText(percentFmt.format(info.getInflationPercent()));
}

/**
 * Updates the data displayed in the text area.
 */
public void updateData()
{
    retireText.setText("");
    MessageFormat retireMsg = new MessageFormat("");
    retireMsg.setLocale(currentLocale);
    retireMsg.applyPattern(resStrings.getString("retire"));

    for (int i = info.getCurrentAge(); i <= info.getDeathAge(); i++)
    {
        Object[] args = { i, info.getBalance(i) };
        retireText.append(retireMsg.format(args) + "\n");
    }
}

/**
 * Updates the graph.
 */
public void updateGraph()
{
    retireCanvas.setColorPre((Color) res.getObject("colorPre"));
    retireCanvas.setColorGain((Color) res.getObject("colorGain"));
    retireCanvas.setColorLoss((Color) res.getObject("colorLoss"));
    retireCanvas.setInfo(info);
    repaint();
}

/**
 * Reads the user input from the text fields.
 */
public void getInfo()
{
    try
    {
        info.setSavings(currencyFmt.parse(savingsField.getText()).doubleValue());
        info.setContrib(currencyFmt.parse(contribField.getText()).doubleValue());
        info.setIncome(currencyFmt.parse(incomeField.getText()).doubleValue());
        info.setCurrentAge(numberFmt.parse(currentAgeField.getText()).intValue());
        info.setRetireAge(numberFmt.parse(retireAgeField.getText()).intValue());
        info.setDeathAge(numberFmt.parse(deathAgeField.getText()).intValue());
        info.setInvestPercent(percentFmt.parse(investPercentField.getText()).doubleValue());
        info.setInflationPercent(
            percentFmt.parse(inflationPercentField.getText()).doubleValue());
    }
    catch (ParseException ex)
    {
        ex.printStackTrace();
    }
}

/**
 * The information required to compute retirement income data.
 */
class RetireInfo
{
    private double savings;
    private double contrib;
    private double income;
    private int currentAge;
    private int retireAge;
    private int deathAge;
    private double inflationPercent;
    private double investPercent;
    private int age;
    private double balance;

    /**
     * Gets the available balance for a given year.
     * @param year the year for which to compute the balance
     * @return the amount of money available (or required) in that year
     */
    public double getBalance(int year)
    {
        if (year < currentAge) return 0;
        else if (year == currentAge)
        {
            age = year;
            balance = savings;
            return balance;
        }
        else if (year == age) return balance;
        if (year != age + 1) getBalance(year - 1);
        age = year;
        if (age < retireAge) balance += contrib;
        else balance -= income;
        balance = balance * (1 + (investPercent - inflationPercent));
        return balance;
    }

    /**
     * Gets the amount of prior savings.
     * @return the savings amount
     */
    public double getSavings()
    {
        return savings;
    }

    /**
     * Sets the amount of prior savings.
     * @param newValue the savings amount
     */
    public void setSavings(double newValue)
    {
        savings = newValue;
    }

    /**
     * Gets the annual contribution to the retirement account.
     * @return the contribution amount
     */
    public double getContrib()
    {
        return contrib;
    }

    /**
     * Sets the annual contribution to the retirement account.
     * @param newValue the contribution amount
     */
    public void setContrib(double newValue)
    {
        contrib = newValue;
    }

    /**
     * Gets the annual income.
     * @return the income amount
     */
    public double getIncome()
    {
        return income;
    }

    /**
     * Sets the annual income.
     * @param newValue the income amount
     */
    public void setIncome(double newValue)
    {
        income = newValue;
    }

    /**
     * Gets the current age.
     * @return the age
     */
    public int getCurrentAge()
    {
        return currentAge;
    }

    /**
     * Sets the current age.
     * @param newValue the age
     */
    public void setCurrentAge(int newValue)
    {
        currentAge = newValue;
    }

    /**
     * Gets the desired retirement age.
     * @return the age
     */
    public int getRetireAge()
    {
        return retireAge;
    }

    /**
     * Sets the desired retirement age.
     * @param newValue the desired retirement age
     */
    public void setRetireAge(int newValue)
    {
        retireAge = newValue;
    }

    /**
     * Gets the expected age of death.
     * @return the age
     */
    public int getDeathAge()
    {
        return deathAge;
    }

    /**
     * Sets the expected age of death.
     * @param newValue the age
     */
    public void setDeathAge(int newValue)
    {
        deathAge = newValue;
    }

    /**
     * Gets the estimated percentage of inflation.
     * @return the percentage
     */
    public double getInflationPercent()
    {
        return inflationPercent;
    }

    /**
     * Sets the estimated percentage of inflation.
     * @param newValue the percentage
     */
    public void setInflationPercent(double newValue)
    {
        inflationPercent = newValue;
    }

    /**
     * Gets the estimated yield of the investment.
     * @return the percentage
     */
    public double getInvestPercent()
    {
        return investPercent;
    }

    /**
     * Sets the estimated yield of the investment.
     * @param newValue the percentage
     */
    public void setInvestPercent(double newValue)
    {
        investPercent = newValue;
    }
}

/**
 * This component draws a graph of the investment result.
 */
class RetireComponent extends JComponent
{
    private static final int PANEL_WIDTH = 400;
    private static final int PANEL_HEIGHT = 200;
    private static final Dimension PREFERRED_SIZE = new Dimension(800, 600);
    private RetireInfo info = null;
    private Color colorPositive;
    private Color colorGain;
    private Color colorLoss;

    public RetireComponent()
    {
        setSize(PANEL_WIDTH, PANEL_HEIGHT);
    }

    /**
     * Sets the retirement information to be plotted.
     * @param newInfo the new retirement info
     */
    public void setInfo(RetireInfo newInfo)
    {
        info = newInfo;
        repaint();
    }

    public void paintComponent(Graphics g)
    {
        Graphics2D g2 = (Graphics2D) g;
        if (info == null) return;

        double minValue = 0;
        double maxValue = 0;
        int i;
        for (i = info.getCurrentAge(); i <= info.getDeathAge(); i++)
        {
            double v = info.getBalance(i);
            if (minValue > v) minValue = v;
            if (maxValue < v) maxValue = v;
        }
        if (maxValue == minValue) return;
```
