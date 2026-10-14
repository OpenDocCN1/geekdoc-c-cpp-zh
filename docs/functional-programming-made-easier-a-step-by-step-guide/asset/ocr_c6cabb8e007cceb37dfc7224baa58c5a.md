```
getMiles :: Address -> Miles
getMiles address = ... ①

getMilesTo :: HasAddress -> Miles
getMilesTo = getMiles $ case _ of ②
  PersonAddress (Person { address }) -> address ③
  CompanyAddress (Company { address }) -> address ④
  ResidenceAddress (Home address) -> address ⑤
  ResidenceAddress (Facility address) -> address ⑥
  EmptyLotAddress (EmptyLot { address }) -> address ⑦
```

① Details aren’t important here.

② Here we call getMiles with the value of the case expression, which is an Address.

③ We pattern match Person and destructure its Record to get the address field.

④ We pattern match Company and destructure its Record to get the address field.

⑤ We pattern match Home.

⑥ We pattern match Facility. Notice we mention ResidenceAddress again here with the only difference being which Residence constructor that we’re matching.

⑦ We pattern match EmptyLot and destructure its Record to get the address field.

With this approach we don’t have to write as many functions, but it’s still a pain to have maintain the Sum Type and update the case expression not just in this function, but every single function that accepts our Sum Type.

# 6.2. The Solution

Everything we’ve done so far is boilerplate code. You know it’s boilerplate when it doesn’t take much thought and you can copy and paste existing solutions and make a few minor edits to get your new function or case.

Copying and pasting should be a red flag that tells you that a more generic solution is desirable and, hopefully, possible. Sometimes though, there are technical limitations that force you to create boilerplate code. But in our case, all we need is some way to specify that Person, Company, Residence and EmptyLot all have addresses.

If they were all Type Aliases for records then we could simply use ._address as our access function (using a wildcard for the Record). But one of these is a Sum Type, viz. Residence, so that won’t work for us.

When we want to treat different things similarly in languages such as C# or Java, we use Interfaces: