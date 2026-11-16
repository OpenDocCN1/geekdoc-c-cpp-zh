# # REGISTERING A DP

Look back at the class diagram of DependencyProperty on page 602. Notice anything missing? There's no constructor. You never actually create an instance of the DependencyProperty class. Instead, you just declare it, and then call one of the versions of the Register...() methods. WPF takes care of all the rest.

There are ten different versions of the Register() method, three overloads of RegisterReadOnly(), three of RegisterAttached(), and two each of RegisterReadOnly() and RegisterAttachedReadOnly(). The signature of each version is shown below.

+   1. Register(<name>, <propertyType>, <ownerType>)
+   2. Register(<name>, <propertyType>, <ownerType>, <PropertyMetadata>)
+   3. Register(<name>, <propertyType>, <ownerType>, <PropertyMetadata>, <ValidateValueCallback>)
+   4. RegisterReadOnly(<name>, <propertyType>, <ownerType>, <PropertyMetadata>)
+   5. RegisterReadOnly(<name>, <propertyType>, <ownerType>, <PropertyMetadata>, <ValidateValueCallback>)
+   6. RegisterAttached(<name>, <propertyType>, <ownerType>)
+   7. RegisterAttached(<name>, <propertyType>, <ownerType>, <PropertyMetadata>)
+   8. RegisterAttached(<name>, <propertyType>, <ownerType>, <PropertyMetadata>, <ValidateValueCallback>)
+   9. RegisterAttachedReadOnly(<name>, <propertyType>, <ownerType>, <PropertyMetadata>)
+   10. RegisterAttachedReadOnly(<name>, <propertyType>, <ownerType>, <PropertyMetadata>, <ValidateValueCallback>)