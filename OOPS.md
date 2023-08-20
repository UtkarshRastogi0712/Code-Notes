### Concepts:

**Four pillars of OOPS are:**
1) Encapsulation
2) Abstraction
3) Polymorphism
4) Inheritance

#### Class: 
- A class is a blueprint of an object like a building block. It is namely comprised of two parts, namely *member functions* and *data members*.
- Class definition does not allocate memory. It is like a user defined datatype allocation.
- Constructors are functions with the same name as the class that may or may not be parameterised and are used to initialise classes to make Objects. A default constructor is always present in a class.
- A copy constructor is used to create an object that is a copy of another. It takes the object to be copied as the parameter and is used using principles of polymorphism.
```C++
class Car{
	public:
	Car(Car &obj){
		make = obj.make;
		speed = obj.speed;
	}
}
```

#### Objects:
- Object is an *instance* of a class.
- It functions like an identifiable entity with *properties (data)* and *behaviour (functions)*.
- Memory is allocated when an object is initialised.
- Objects interact by sending messages to each other without having details about the exact content in one another.

#### Encapsulation:
- *Wrapping/binding* data along with the functions that can manipulate them in one single unit.
- Encapsulation is implemented with *namespaces*, that are declarative regions which *provide scope* to the identifiers in the region to prevent *name collisions*.
- There are *Built-in, global and local namespaces* that store built-in keywords, global and local identifiers respectively.
- The lifetime of a namespace is active for as long as objects of the namespace exist and are alive/in-use.
- Namespace resolution for function defined outside class:
```C++
class Car{
	public:
	void brake();
}
void Car::brake(){
	return declerate;
}
```

#### Abstraction:
- Abstraction simply means *data hiding* or showing only essential features and details.
- Abstraction can be implemented by using classes, to model real usable objects by hiding internal working and data or by using header files to import necessary functions without delving into redesigning the wheel.
- Abstraction is also the use of encapsulation to hide data that is not necessary to understand the application.
> Access specifiers also help us with data hiding,
> - *Public:* All class members can be accessed by other classes and functions.
> - *Private:* Only friend functions can access data members of class apart from internal members.
> - *Protected:* Class members, subclasses and friend classes can access data members and functions.
```C++
class Car{
	public:
	friend class Truck;
	friend void show();
}
class Truck{
}
void show(){
}
```

#### Polymorphism:
- It refers to *having multiple forms* or the ability of a singular function/application to take multiple forms.
- *Operator overloading:* Making a built-in operator take different forms in different classes by overloading its functionality. It doesnt take away old functionality, just adds new functionality with context to objects.

> *Note:* Not all operators can be overloaded in C++. Namely, pointer/member access( . ,* ) , scope resolution( :: ), typeid, sizeof, ternary ( ? : ) operator cannot be overloaded.

```C++
Complex operator+(Complex const& obj1, Complex const& obj2){
	Complex res;
	res.real = obj1.real + obj2.real;
	res.img = obj1.img + obj2.img;
	return res;
}
```

- *Function overloading:* Making a function of the same name perform multiple functions by changing its function signature (accepted arguments)

> Rules for a different function signature:
>  - Different types in arguments
>  - Different number of arguments
>  - Different sequence of arguments of different types
>  
>  Rules for matching function signature:
>  - Exact parameter list match
>  - By implicit type conversion
>  - By standard conversion and default values

##### Runtime overloading vs compile time overloading: 
- Compile time overloading occurs at compiling stage when compiler matches method signature of functions with the same name.
- Runtime overloading *(overriding)* occurs during execution using virtual functions and abstract classes with same function names through parent and child classes where the function to be used is determined at runtime
- Abstract classes are classes with at least one pure virtual function, while virtual function is a function that can be overridden by polymorphism from a child class. Both serve as templates.
```C++
class Car{
	virtual void show() = 0;
}
class Brake : public Car{
	void show(){
	}
}
int main(){
	Car* c = new Brake;
	c->show();
}
```
#### Inheritance:
- Inheritance adds the concept of *reusability of code* where we can derive child classes from parents classes to extend functionality.
```C++
class Car{
	<statements>
}
class Brake : public Car{
	<statements>
}
```
> Types of inheritance :
> - Single (Parent to child)
> - Multilevel (Chain linked parents and children)
> - Multiple (Multiple parents to one child)
> - Hierarchical (Multiple levels in a tree)
> - Hybrid (Mix of multiple)
