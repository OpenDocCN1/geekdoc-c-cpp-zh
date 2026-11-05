Generated JWT:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

Token is valid. User: JohnDoe

JWTs contain 3 parts: Header, Payload, and Signature.

+   - The Header includes the signing algorithm (e.g., HS256).
+   - The Payload holds claims (user info, expiration time).
+   - The Signature ensures the token hasn't been tampered with.
+   - JWTs are usually passed in HTTP headers as: Authorization: Bearer <token>.
+   - Validating a JWT checks its signature, expiration, and other claims.
+   - Do NOT hard-code secrets in production apps—use secure vaults or environment variables.

# [Supplement]

+   - JWTs are stateless: no session storage needed on server.
+   - The payload is Base64-encoded, not encrypted—never store sensitive data inside.
+   - You can decode JWTs using tools like jwt.io to inspect them manually.