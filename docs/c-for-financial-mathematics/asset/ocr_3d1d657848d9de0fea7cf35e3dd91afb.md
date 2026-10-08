+   6. normcdf(0) should be equal to 0.5.

+   7. normcdf(norminv(x)) should equal x.

+   8. normcdf(1.96) \approx 0.975. This is just a well-known fact: it is worth remembering as it enables you to quickly compute 95% confidence intervals.

+   9. \(\mathrm{normcdf}(x)=\int_{-\infty}^{x} \frac{1}{\sqrt{2 \pi}} \exp \left(-\frac{x^{2}}{2}\right) \mathrm{d} x\). So it should be possible to test the value of normcdf by computing the integral directly using numerical integration.

Here is the code that runs all these tests but the last:

```
static void testNormCdf() {
  // test bounds
  ASSERT(normcdf(0.3)>0);
  ASSERT(normcdf(0.3)<1);
  // test extreme values
  ASSERT_APPROX_EQUAL(normcdf(-1e10), 0, 0.001);
  ASSERT_APPROX_EQUAL(normcdf(1e10), 1.0, 0.001);
  // test increasing
  ASSERT(normcdf(0.3)<normcdf(0.5));
  // test symmetry
  ASSERT_APPROX_EQUAL(normcdf(0.3),
                      1 - normcdf(-0.3), 0.0001);
  ASSERT_APPROX_EQUAL(normcdf(0.0), 0.5, 0.0001);
  // test inverse
  ASSERT_APPROX_EQUAL(normcdf(norminv(0.3)),
                      0.3, 0.0001);
  // test well known value
  ASSERT_APPROX_EQUAL(normcdf(1.96), 0.975, 0.001);
}
```

As this demonstrates, writing test code is usually much easier than thinking of tests in the first place. Nevertheless, some tests (e.g., computing **normcdf** by integration) can require quite a bit of work. However, if you are planning to invest real money on the basis of the answers your code produces, or if you are planning to publish a journal article based on your calculations, you should always make sure that you test them as thoroughly as possible.

If you look at the testing code, you will see that we have only tested a few specific cases of the claim normcdf(x) > 0. This is all that is needed. Our tests give us a great deal of confidence in our code even though we have by no means proved it worked in all cases. When you write a test you should be trying to write a quick simple check and not a mathematical proof.

These different ideas for how to test normcdf can be generalised to test many other functions. The last option is the most obvious but is also, in some