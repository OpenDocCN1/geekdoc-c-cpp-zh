```
```java
public class RentalCalculator {
    private List<Rental> rentals = new ArrayList<>();

    public void addRental(String title, int days) {
        rentals.add(new Rental(title, days));
    }

    public int getRentalFee() {
        int fee = 0;
        for (Rental rental : rentals)
            fee += rental.getFee();
        return fee;
    }

    public int getRenterPoints() {
        int points = 0;
        for (Rental rental : rentals)
            points += rental.getPoints();
        return points;
    }
}

public List<Paycheck> run(Database db) {
    Calendar now = SystemTime.getCurrentDate();
    List<Paycheck> paychecks = new ArrayList<>();
    for (Employee e : db.getAllEmployees()) {
        if (e.isPayDay(now))
            paychecks.add(e.calculatePay());
    }

    return paychecks;
}
```
```