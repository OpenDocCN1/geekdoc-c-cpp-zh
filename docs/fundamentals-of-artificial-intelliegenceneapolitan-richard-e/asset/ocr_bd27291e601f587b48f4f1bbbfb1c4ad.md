# Table 2.4 A Subset of the Rules in a System for Bagging Groceries

+   1. IF step is Bag_large_items AND there is a large item to be bagged AND there is a large bottle to be bagged AND there is a bag with <6 items THEN put the large bottle in the bag.
+   
+   2. IF step is Bag_large_items AND there is a large item to be bagged AND there is a bag with <6 items THEN put the large item in the bag.
+   
+   3. IF step is Bag_large_items AND there is a large item to be bagged THEN start a fresh bag.
+   
+   4. IF step is Bag_large_items THEN step is Bag_medium_items.
+   
+   5. IF step is Bag_medium_items AND there is a medium item to be bagged AND there is a bag with <10 medium items AND that bag contains 0 large items AND the medium item is frozen AND the medium item is not in an insulated bag THEN put the medium item in an insulated bag.
+   
+   6. IF step is Bag_medium_items AND there is a medium item to be bagged AND there is a bag with <10 medium items AND that bag contains 0 large items THEN put the medium item in the bag.
+   
+   7. IF step is Bag_medium_items AND there is a medium item to be bagged THEN start a fresh bag.
+   
+   8. IF step is Bag_medium_items THEN step is Bag_small_items.
+   
+   9. IF step is Bag_small_items AND there is a small item to be bagged AND there is a bag that is not full THEN put the small item in the bag.
+   
+   10. IF step is Bag_small_items AND there is a small item to be bagged THEN start a fresh bag.
+   
+   11. IF step is Bag'\_small\_items THEN halt.