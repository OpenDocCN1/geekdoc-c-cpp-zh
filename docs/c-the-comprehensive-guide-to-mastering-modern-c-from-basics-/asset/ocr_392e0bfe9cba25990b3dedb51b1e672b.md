A new called in this way never throws an exception (although the called constructor might). Instead, it returns a nullptr in the case of an error.

> Tip
Prefer RAII when designing your objects: write code that utilizes RAII.