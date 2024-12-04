#### OOP Terminology

## Abstract Classes:
These are classes that cannot be instantiated on their own and are typically used as base classes. They contain at least one pure virtual function, which forces derived classes to provide an implementation for these functions, thus implementing specific behaviors.
## Interfaces:
In C++, an interface can be simulated using a class where all methods are pure virtual. Interfaces define a set of methods that derived classes must implement, ensuring a consistent API regardless of the specific object's type.
## Abstraction:
Abstraction involves hiding the complex reality while exposing only the necessary parts of an object. It helps in reducing programming complexity and increasing efficiency.
## Access Modifiers:
These keywords control how members (variables, methods) of a class can be accessed.
# Public: Members are accessible from any part of the program.
# Private: Members cannot be accessed (or viewed) from outside the class.
# Protected: Members cannot be accessed from outside the class, except by inherited classes.
## Attributes/Properties:
These are data members of a class that hold data specific to an object and define its state. Properties can have public, protected, or private visibility.
## Class Variables:
These are static members of a class, shared among all instances of the class. They represent global properties of a class.
## Classes and Objects:
A class is a blueprint for creating objects (a particular data structure), providing initial values for state (member variables) and implementations of behavior (member functions or methods). An object is an instance of a class.
## Collections and Iterators:
Collections are data structures that hold objects. Iterators are used to navigate through collections.
## Compostion:
A design principle where a class includes instances of other classes inside itself to provide enhanced functionality. This differs from inheritance and is often used to express a "has-a" relationship.
## Constructors and Destructors:
Constructors are special class functions which are executed whenever a new object of that class is created. They generally initialize the attributes of the new object. Destructors are special functions executed when an object is destroyed or deleted. They are used to perform cleanup before the object is deallocated.
## Encapsulation:
The act of restricting access to some of the object's components, which means that the internal representation of an object is generally hidden from view outside of the object’s definition. Access to the data and methods is tightly controlled by an interface.
## Exception Handiling:
Mechanism to handle runtime errors, providing a way to react to exceptional circumstances (like runtime errors) in programs by transferring control to special functions called handlers.
## Generics and Templates:
Templates in C++ are a powerful feature that allows you to write generic programs that work with any data type. It enables the creation of functions and classes that can work with any data type without being rewritten for each type.
## Inheritance:
It is a mechanism wherein a new class is derived from an existing class. The derived class inherits all the features from the base class, adding new features or modifying existing ones.
## Method Overloading:
This involves having multiple methods in the same scope, with the same name but different parameters.
## Polymorphism:
The ability of a message to be displayed in more than one form. A person at the same time can have different characteristics. Similarly, a method in a child class can have a different implementation than a method in the parent class, which it overrides.
## Static(Methods and Variables):
Static variables are used to store common data across all class instances, and static methods are accessed without creating an instance of the class.
## UML Diagrams and Modeling:
UML (Unified Modeling Language) is a standardized modeling language enabling developers to specify, visualize, construct, and document artifacts of software systems, as well as for business modeling. UML diagrams represent classes, objects, interfaces, and their relationships.
