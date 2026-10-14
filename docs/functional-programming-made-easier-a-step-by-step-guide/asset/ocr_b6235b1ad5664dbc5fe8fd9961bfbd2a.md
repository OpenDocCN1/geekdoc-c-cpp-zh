![](bbox=[0.32, 0.06, 0.68, 0.39])

Notice that Morphisms between Objects a and b are Pure Functions, i.e. f :: a -> b. We can compose Pure Functions as is shown in the diagram. Here we compose pure with f to product a Monadic Function, pure <<< f :: a -> m b.

Now let's look at Kleisli:

![](bbox=[0.32, 0.51, 0.68, 0.83])

Unlike the Hask Category, in the Kleisli Category, a Morphism between a and b has the Type Signature of a -> m b. These Morphisms are formally known as Kleisli Arrows.

We can show that Kleisli is a valid Cateogory if we can prove the Category Laws: