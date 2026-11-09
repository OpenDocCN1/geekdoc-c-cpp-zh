
```java
public class SineTaylorCalculator {
    public double calculateTerm(double r, int n) {
        int sign = calcSign(n-1);
        double power = calcPower(r, 2*n-1);
        double factorial = calcFactorial(2*n-1);
        return sign*power/factorial;
    }

    protected double calcFactorial(int n) {
        double fac = 1;
        for (int i=1; i<=n; i++)
            fac *= i;
        return fac;
    }

    protected double calcPower(double r, int n) {
        double power = 1;
        for (int i=0; i<n; i++)
            power *= r;
        return power;
    }

    protected int calcSign(int n) {
        int sign = 1;
        for (int i=0; i<n; i++)
            sign *= -1;
        return sign;
    }
}
```

```java
package London_sine;

public class SineTaylorCalculatorSpy extends SineTaylorCalculator {
    private int fac_n;
    private double power_r;
    private int power_n;
    private int sign_n;
    public double getR() {
        return power_r;
    }

    public int getRPower() {
        return power_n;
    }

    public int getFac() {
        return fac_n;
    }

    public int getSignPower() {
        return sign_n;
    }

    protected double calcFactorial(int n) {
        fac_n = n;
        return super.calcFactorial(n);
    }

    protected double calcPower(double r, int n) {
        power_r = r;
        power_n = n;
        return super.calcPower(r, n);
    }

    protected int calcSign(int n) {
        sign_n = n;
        return super.calcSign(n);
    }

    public double calculateTerm(double r, int n) {
        return super.calculateTerm(r, n);
    }
}
```

```java
public double sin(double r) {
    double sin=0;
    for (int n=1; n<10; n++)
        sin += calculateTerm(r, n);
    return sin;
}

@Test
public void testSineInRange() throws Exception {
    SineTaylorCalculator c = new SineTaylorCalculator();
    for (int i=0; i<100; i++) {
        double r = (Math.random() * 4 * PI) - (2 * PI);
        double sinr = c.sin(r);
        assertTrue(sinr < 1 && sinr > -1);
    }
}

public double cos(double r) {
    return (sin(r+PI/2));
}

@Test
public void PythagoreanIdentity() throws Exception {
    SineTaylorCalculator c = new SineTaylorCalculator();
    for (int i=0; i<100; i++) {
        double r = (Math.random() * 4 * PI) - (2 * PI);
        double sinr = c.sin(r);
        double cosr = c.cos(r);
        assertEquals(1.0, sinr * sinr + cosr * cosr, 0.00001);
    }
}
```

```java
@Test
public void sineValues() throws Exception {
    checkSin(0, 0);
    checkSin(PI, 0);
    checkSin(PI/2, 1);
    checkSin(PI/3, 0.8660254038);
    checkSin(PI/4, 0.7071067812);
    checkSin(PI/5, 0.5877852523);
}
```

```java
struct SteeringPresentationElement {
    int steps;
    bool direction;
    int stepTime;
    int delay;
};

public class CustomerTest {
    @Test
    public void RegularMovie_OneDay() throws Exception {
        Customer c = new Customer();
        c.addRental("RegularMovie", 1);
        assertEquals(1.5, c.getRentalFee(), 0.001);
        assertEquals(1, c.getRenterPoints());
    }
}

public class Customer {
    public void addRental(String title, int days) {
    }

    public double getRentalFee() {
        return 1.5;
    }

    public int getRenterPoints() {
        return 1;
    }
}
```

```java
public class CustomerTest {
    private Customer customer;

    @Before
    public void setUp() throws Exception {
        customer = new Customer();
    }

    private void assertFeeAndPoints(double fee, int points) {
        assertEquals(fee, customer.getRentalFee(), 0.001);
        assertEquals(points, customer.getRenterPoints());
    }

    @Test
    public void RegularMovie_OneDay() throws Exception {
        customer.addRental("RegularMovie", 1);
        assertFeeAndPoints(1.5, 1);
    }

    @Test
    public void RegularMovie_SecondAndThirdDayFree() throws Exception {
        customer.addRental("RegularMovie", 2);
        assertFeeAndPoints(1.5, 1);
        customer.addRental("RegularMovie", 3);
        assertFeeAndPoints(1.5, 1);
    }

    @Test
    public void RegularMovie_FourDays() throws Exception {
        customer.addRental("RegularMovie", 4);
        assertFeeAndPoints(3.0, 2);
    }
}
```

```java
public class Customer {
    private int days;

    public void addRental(String title, int days) {
        this.days = days;
    }

    public double getRentalFee() {
        double fee = 1.5;
        if (days > 3)
            fee += 1.5 * (days - 3);
        return fee;
    }

    public int getRenterPoints() {
        int points = 1;
        if (days > 3)
            points += (days - 3);
        return points;
    }
}
```

```java
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

```java
public class CustomerTest {
    private Customer customer;

    @Before
    public void setUp() throws Exception {
        customer = new Customer();
    }

    private void assertFeeAndPoints(int fee, int points) {
        assertEquals(fee, customer.getRentalFee());
        assertEquals(points, customer.getRenterPoints());
    }

    @Test
    public void RegularMovie_OneDay() throws Exception {
        customer.addRental("RegularMovie", 1);
        assertFeeAndPoints(150, 1);
    }

    @Test
    public void RegularMovie_SecondAndThirdDayFree() throws Exception {
        customer.addRental("RegularMovie", 2);
        assertFeeAndPoints(150, 1);
        customer.addRental("RegularMovie", 3);
        assertFeeAndPoints(150, 1);
    }

    @Test
    public void RegularMovie_FourDays() throws Exception {
        customer.addRental("RegularMovie", 4);
        assertFeeAndPoints(300, 2);
    }
}
```

```java
@Test
public void ChildrensMovie_OneDay() throws Exception {
    customer.addRental("ChildrensMovie", 1);
    assertFeeAndPoints(100, 1);
}

public int getRentalFee() {
    if (title.equals("RegularMovie"))
        return applyGracePeriod(150, 3);
    else
        return 100;
}
```

```java
public class Customer {
  private String title;
  private int days;
  private Map<String, VideoType> movieRegistry = new HashMap<>();

  enum VideoType {REGULAR, CHILDRENS};

  public Customer() {
    movieRegistry.put("RegularMovie", REGULAR);
    movieRegistry.put("ChildrensMovie", CHILDRENS);
  }

  public void addRental(String title, int days) {
    this.title = title;
    this.days = days;
  }

  public int getRentalFee() {
    if (getType(title) == REGULAR)
      return applyGracePeriod(150, 3);
    else
      return 100;
  }

  private VideoType getType(String title) {
    return movieRegistry.get(title);
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

```java
public class VideoRegistry {
    public enum VideoType {REGULAR, CHILDRENS}

    private static Map<String, VideoType> videoRegistry =
            new HashMap<>();

    public static VideoType getType(String title) {
        return videoRegistry.get(title);
    }

    public static void addMovie(String title, VideoType type) {
        videoRegistry.put(title, type);
    }
}

@BeforeClass
public static void loadRegistry() {
    VideoRegistry.addMovie("RegularMovie", REGULAR);
    VideoRegistry.addMovie("ChildrensMovie", CHILDRENS);
}
```

```java
public class Customer {
    private String title;
    private int days;

    public void addRental(String title, int days) {
        this.title = title;
        this.days = days;
    }

    public int getRentalFee() {
        if (VideoRegistry.getType(title) == REGULAR)
            return applyGracePeriod(150, 3);
        else
            return 100;
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

@Test
public void ChildrensMovie_FourDays() throws Exception {
    customer.addRental("ChildrensMovie", 4);
    assertFeeAndPoints(400, 1);
}
```
