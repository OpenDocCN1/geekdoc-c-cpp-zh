```
import javax.security.auth.login.*;
import com.sap.security.auth.login.LoginContextFactory;

public class LoginServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request,
                         HttpServletResponse response)
            throws ServletException, IOException {
        // Trigger a form-based login as necessary:
        if (request.getUserPrincipal() == null) {
            try {
                LoginContext ctx =
                        LoginContextFactory.createLoginContext("FORM");
                ctx.login();
            } catch (LoginException le) {
                // TODO: Error handling...
            }
        }

        response.getWriter().println("Hello, " +
                request.getUserPrincipal().getName());
    }
}
```

# Listing 8.8 Triggering a Form-Based Login Using the Authentication API

To log a user out, simply call the `logout()` method of the `LoginContext` interface, as shown in Listing 8.9. That's pretty much all there is to it. However, if you're)
            throws ServletException, IOException {
        try {
            LoginContext ctx =
                    LoginContextFactory.createLoginContext();
            ctx.logout();
        }
    }
}