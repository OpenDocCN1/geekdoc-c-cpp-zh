# 12.3. Type Variance in Generics

In C#, type variance enables implicit reference conversion for array types, delegate types, and generic type parameters so that broader, or more specific, types can be used. Variances, either covariance or contravariance, are supported for reference types, but they are not supported for value types.