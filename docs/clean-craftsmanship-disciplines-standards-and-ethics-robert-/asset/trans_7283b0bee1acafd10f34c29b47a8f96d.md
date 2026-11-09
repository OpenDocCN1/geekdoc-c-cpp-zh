
```java
@Test
public void whenClosed_loginIsCancelled() throws Exception {
  Authenticator authenticator = new AuthenticatorDummy();
  LoginDialog dialog = new LoginDialog(authenticator);
  dialog.show();
  boolean success = dialog.sendEvent(Event.CLOSE);
  assertTrue(success);
}

public void whenAuthorizerRejects_loginFails() throws Exception {
  Authenticator authenticator = new ?();
  LoginDialog dialog = new LoginDialog(authenticator);
  dialog.show();
  boolean success = dialog.submit("bad username", "bad password");
  assertFalse(success);
}

public class RejectingAuthenticator implements Authenticator {
  public Boolean authenticate(String username, String password) {
    return false;
  }
}

public void whenAuthorizerRejects_loginFails() throws Exception {
  Authenticator authenticator = new RejectingAuthenticator();
  LoginDialog dialog = new LoginDialog(authenticator);
  dialog.show();
  boolean success = dialog.submit("bad username", "bad password");
  assertFalse(success);
}
```

```java
public class PromiscuousAuthenticator implements Authenticator {
    public Boolean authenticate(String username, String password) {
        return true;
    }
}
@Test
public void whenAuthorizerAccepts_loginSucceeds() throws Exception {
    Authenticator authenticator = new PromiscuousAuthenticator();
    LoginDialog dialog = new LoginDialog(authenticator);
    dialog.show();
    boolean success = dialog.submit("good username", "good password");
    assertTrue(success);
}

public class AuthenticatorSpy implements Authenticator {
    private int count = 0;
    private boolean result = false;
    private String lastUsername = "";
    private String lastPassword = "";

    public Boolean authenticate(String username, String password) {
        count++;
        lastPassword = password;
        lastUsername = username;
        return result;
    }

    public void setResult(boolean result) {this.result = result;}
    public int getCount() {return count;}
    public String getLastUsername() {return lastUsername;}
    public String getLastPassword() {return lastPassword;}
}
```

```java
@Test
public void loginDialog_correctlyInvokesAuthenticator() throws Exception {
  AuthenticatorSpy spy = new AuthenticatorSpy();
  LoginDialog dialog = new LoginDialog(spy);
  spy.setResult(true);
  dialog.show();
  boolean success = dialog.submit("user", "pw");
  assertTrue(success);
  assertEquals(1, spy.getCount());
  assertEquals("user", spy.getLastUsername());
  assertEquals("pw", spy.getLastPassword());
}

public class AuthenticatorMock extends AuthenticatorSpy {
  private String expectedUsername;
  private String expectedPassword;
  private int expectedCount;

  public AuthenticatorMock(String username, String password,
                           int count) {
    expectedUsername = username;
    expectedPassword = password;
    expectedCount = count;
  }

  public boolean validate() {
    return getCount() == expectedCount &&
      getLastPassword().equals(expectedPassword) &&
      getLastUsername().equals(expectedUsername);
  }
}
```

```java
@Test
public void loginDialogCallToAuthenticator_validated() throws Exception {
    AuthenticatorMock mock = new AuthenticatorMock("Bob", "xyzzy", 1);
    LoginDialog dialog = new LoginDialog(mock);
    mock.setResult(true);
    dialog.show();
    boolean success = dialog.submit("Bob", "xyzzy");
    assertTrue(success);
    assertTrue(mock.validate());
}

@Test
public void badPasswordAttempt_loginFails() throws Exception {
    Authenticator authenticator = new FakeAuthenticator();
    LoginDialog dialog = new LoginDialog(authenticator);
    dialog.show();
    boolean success = dialog.submit("user", "bad password");
    assertFalse(success);
}

@Test
public void goodPasswordAttempt_loginSucceeds() throws Exception {
    Authenticator authenticator = new FakeAuthenticator();
    LoginDialog dialog = new LoginDialog(authenticator);
    dialog.show();
    boolean success = dialog.submit("user", "good password");
    assertTrue(success);
}
```

```java
public class FakeAuthenticator implements Authenticator {
  public Boolean authenticate(String username, String password)
  {
    return (username.equals("user") &&
            password.equals("good password"));
  }
}
```

```java
public class SineTest {
  private static final double EPSILON = 0.0001;
  @Test
  public void sines() throws Exception {
    assertEquals(0, sin(0), EPSILON);
  }

  double sin(double radians) {
    return 0.0;
  }
}
```

```java
public class SineTest {
  private static final double EPSILON = 0.0001;
  @Test
  public void sines() throws Exception {
    assertEquals(0, sin(0), EPSILON);
    assertEquals(0, sin(Math.PI), EPSILON);
  }

  double sin(double radians) {
    return 0.0;
  }
}
```

```java
public class SineTest {
    private static final double EPSILON = 0.0001;
    @Test
    public void sines() throws Exception {
        assertEquals(0, sin(0), EPSILON);
        assertEquals(0, sin(Math.PI), EPSILON);
        assertEquals(1, sin(Math.PI/2), EPSILON);
    }
    double sin(double radians) {
        return 0.0;
    }
}
```

```java
public class SineTest {
    private static final double EPSILON = 0.0001;
    @Test
    public void sines() throws Exception {
        assertEquals(0, sin(0), EPSILON);
        assertEquals(0, sin(Math.PI), EPSILON);
        assertEquals(1, sin(Math.PI/2), EPSILON);
    }

    double sin(double radians) {
        double r2 = radians * radians;
        double r3 = r2*radians;
        double r5 = r3 * r2;
        double r7 = r5 * r2;
        double r9 = r7 * r2;
        double r11 = r9 * r2;
        double r13 = r11 * r2;
        return (radians - r3/6 + r5/120 - r7/5040 + r9/362880 -
                r11/39916800.0 + r13/6227020800.0);
    }
}

public void sines() throws Exception {
    assertEquals(0, sin(0), EPSILON);
    assertEquals(0, sin(Math.PI), EPSILON);
    assertEquals(1, sin(Math.PI/2), EPSILON);
    assertEquals(0.8660, sin(Math.PI/3), EPSILON);
    assertEquals(0.7071, sin(Math.PI/4), EPSILON);
    assertEquals(0.5877, sin(Math.PI/5), EPSILON);
}
```

```java
public class SineTest {
    private static final double EPSILON = 0.000000001;
    @Test
    public void sines() throws Exception {
        assertEquals(0, sin(0), EPSILON);
        assertEquals(0, sin(Math.PI), EPSILON);
        assertEquals(1, sin(Math.PI/2), EPSILON);
        assertEquals(0.8660254038, sin(Math.PI/3), EPSILON);
        assertEquals(0.7071067812, sin(Math.PI/4), EPSILON);
        assertEquals(0.5877852523, sin(Math.PI/5), EPSILON);
    }

    double sin(double radians) {
        double result = radians;
        double lastResult = 2;
        double m1 = -1;
        double sign = 1;
        double power = radians;
        double fac = 1;
        double r2 = radians * radians;
        int n = 1;
        while (!close(result, lastResult)) {
            lastResult = result;
            power *= r2;
            fac *= (n+1) * (n+2);
            n += 2;
            sign *= m1;
            double term = sign * power / fac;
            result += term;
        }

        return result;
    }

    boolean close(double a, double b) {
        return Math.abs(a - b) < .0000001;
    }
}
```

```java
private void checkSin(double radians, double sin) {
    assertEquals(sin, sin(radians), EPSILON);
}

@Test
public void sines() throws Exception {
    checkSin(0, 0);
    checkSin(PI, 0);
    checkSin(PI/2, 1);
    checkSin(PI/3, 0.8660254038);
    checkSin(PI/4, 0.7071067812);
    checkSin(PI/5, 0.5877852523);

    checkSin(3* PI/2, -1);
}

checkSin(1000*PI + PI/3, sin(PI/3));

@Test
public void taylorTerms() throws Exception {
    SineTaylorCalculatorSpy c = new SineTaylorCalculatorSpy();
    double r = Math.random() * PI;
    for (int n = 1; n <= 10; n++) {
        c.calculateTerm(r, n);
        assertEquals(n - 1, c.getSignPower());
        assertEquals(r, c.getR(), EPSILON);
        assertEquals(2 * n - 1, c.getRPower());
        assertEquals(2 * n - 1, c.getFac());
    }
}
```
