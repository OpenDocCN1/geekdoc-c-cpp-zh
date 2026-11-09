```
public class Customer {
    private int days;

    public void addRental(String title, int days) {
        this.days = days;
    }

    public int getRentalFee() {
        return applyGracePeriod(150, 3);
    }

    public int getRenterPoints() {
        return applyGracePeriod(1, 3);
    }

    private int applyGracePeriod(int amount, int grace) {
        if (days > grace)
            return amount + amount * (days - grace);
        return amount;
    }
}
```

**Red:** We want to use `applyGracePeriod` for both the renter points and the fee, but the fee is a `double`, and the points are an `int`. Money should never be a `double`! So, we changed the fee into an `int`, and all the tests broke. We need to go back and fix all our tests.

[Click here to view code image]()

```
public class CustomerTest {
    private Customer customer;

    @Before
    public void setUp() throws Exception {
        customer = new Customer();
    }

    private void assertFeeAndPoints(int fee, int points) {
        assertEquals(fee, customer.getRentalFee());
```