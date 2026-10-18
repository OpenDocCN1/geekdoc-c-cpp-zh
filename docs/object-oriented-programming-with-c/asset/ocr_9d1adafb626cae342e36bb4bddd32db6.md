164. Do not use implicit type conversions unless it is necessary. If they are used arbitrarily, it can cause problems for future users of the class.

165. Whenever we use **new** in a constructor to allocate memory, we should use **delete** in the corresponding destructor to free that memory.

166. The relationship “is __________ a” indicates inheritance. For example, a car is a kind of vehicle.

167. The relationship “has __________ a” indicates containment. For example, a car has an engine. Aggregate objects are constructed using containment.

168. Both inheritance and containment facilitate software reuse.

169. A new class that is created from an existing class using the principle of inheritance is called a _derived class_ or _subclass_. The parent class is called the _base class_ or _superclass_.

170. When an object that is an instance of derived class, is instantiated, the constructor for the base class is invoked before the body of the constructor for the derived class is invoked.

171. A class intended to be a base class usually should use **protected** instead of **private** members.

172. When a derived class object is being created, first its base classes constructors are called before its own constructor. The destructors are called in the reverse order.

173. A constructor of a derived class must pass the arguments required by its base class constructor.

174. A derived class uses the member functions of the base class unless the derived class provides a replacement function with the same name.

175. A derived class object is converted to a base class object when used as an argument to a base class member function.

176. Derived class constructors are responsible for initializing any data members added to those inherited from the base class.