data member `m_Damage`. You can derive a new class `Boss` from `Enemy` for a boss. This means that `Boss` could automatically have `Attack()` and `m_Damage` without you having to write any code for them at all. Then, to make a boss tough, you could add a member function `SpecialAttack()` and a data member `DamageMultiplier` to the `Boss` class. Take a look at Figure 10.1, which shows the relationship between the `Enemy` and `Boss` classes.

![](bbox=[0.1, 0.28, 0.28, 0.71])

Figure 10.1
`Boss` inherits `Attack()` and `m_Damage` from `Enemy` while defining `SpecialAttack()` and `m_DamageMultiplier`.

One of the many advantages of inheritance is that you can reuse classes you’ve already written. This reusability produces benefits that include:

+   - **Less work.** There’s no need to redefine functionality you already have. Once you have a class that provides the base functionality for other classes, you don’t have to write that code again.
+   - **Fewer errors.** Once you’ve got a bug-free class, you can reuse it without errors cropping up in it.