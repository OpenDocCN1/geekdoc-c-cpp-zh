```
/* Now a class method is called, like this */
ObjectReference.MethodName();
Next, we can see the instance variables and methods in a class are accessed:
public class Puppy {
int PuppyAge;
public Puppy(String name) {
// This constructor contains a single parameter called name.
System.out.println("Name chosen is :" + name );
}
public void setAge(int age) {
PuppyAge = age;
}
public int getAge() {
System.out.println("Puppy's age is :" + PuppyAge );
return PuppyAge;
}
public static void main(String[] args) {
/* Object creation */
Puppy myPuppy = new Puppy( "fluffy" );
/* Now we call the class method to set the Puppy's age */
myPuppy.setAge(2);
/* Next, we call another class method to get the Puppy's age */
```