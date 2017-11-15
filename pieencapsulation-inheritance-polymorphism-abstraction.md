# Encapsulation

The process of combining all of an object's attributes and methods into a single package.

**Information Hiding** or **Data Hiding**

* other classes should not alter an object's attribute

### Life Example:

**Car** does not need to tell driver/user how it burns fuel, how the transmission is working.   
_It conceals those details. _  
All user have to know is those exposed to them, e.g. how to accelerate, break and steer.

### Code Example:

Some languages have features which allow us to enforce encapsulation strictly. In Java or C++, we can define access permissions on object attributes, and make it illegal for them to be accessed from outside the object's methods. In Java it is also considered good practice to write **setters and getters** for all attributes, even if the getter simply retrieves the attribute and the setter just assigns it the value of the parameter which you pass in.

In Python, encapsulation is not enforced by the language, but there is a convention that we can use to indicate that a property is intended to be private and is not part of the object's public interface: we begin its name with an underscore.

| Attribute Name | Notation | Behavior |
| :--- | :--- |:--- |
| name  | Public | Can be accessed from inside and outside |
| _name  | Protected | Like a public member, but shouldn't be directly accessed from outside |
| __name  | Private | Can't be seen and accessed from outside |

```py
class Car(object):
    def __init__(self, steel_degree, fuelEfficiency, transmission):
        self.steel = steel_degree
        self._fuelEfficiency = fuelEfficiency
        self.__transmission = transmission
    def getter(self):
        return sth
    def setter(self):
        #set sth
```
---
# Inheritance

Inheritance is a relationship between classes. It is a "is-a" relation.
Subclass can invoke attributes and methods in superclass.
That is, inheritance allows the child class to inherit the attributes and behaviors of its parent.

```py
class Person:
    def somefunction:
        stuff
class GreenObject:
    stuff
#Inheritance
class Man(Person):
    stuff
#multiple inheritance
class ManWithGreenHat(Man,GreenObject):
    stuff
```
---

# Polymorphism

Polymorphism is the ability of one object to be treated and used like another object. 
For example, we treat duck as an animal and not just as a duck. Similarly we treat dog and cat also as animals.

Static (object oriented) Languages like Java and C++ has traditional polymorphism as we need to stick with types and define operations specific to the interpreter. 

Yet in Python like dynamic languages, polymorphism is almost everywhere.

### Traditional Polymorphism
```py
class Animal:
    def Name(self):
        stuff
    def Speak(self):
        stuff

class Dog(Animal):
    def Name(self):
        stuff
    def Speak(self):
        print ("woof!")
        
class Cat(Animal):
    def Name(self):
        stuff
    def Speak(self):
        print ("Meow~")
        
class Lion(Animal):
    def Name(self):
        stuff
    def Speak(self):
        print ("Roar!")
```
### Dynamic Python
Python is strongly typed as the interpreter keeps track of all variables types. 

For example:  variables can support any objects which support ‘add’ operation. Not only integer but also string, list, tuple and dictionary can realize their relative ‘add’ operation

```py
1+2
'abc' + 'cdf'
[1,2,3] + ['c', 'e', 'f']
```

