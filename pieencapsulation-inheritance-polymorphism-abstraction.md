# Encapsulation

The process of combining all of an object's attributes and methods into a single package.

**Information Hiding** or **Data Hiding**
- other classes should not alter an object's attribute

### Life Example:
**Car** does not need to tell driver/user how it burns fuel, how the transmission is working. 
*It conceals those details. *
All user have to know is those exposed to them, e.g. how to accelerate, break and steer.

### Code Example:
Some languages have features which allow us to enforce encapsulation strictly. In Java or C++, we can define access permissions on object attributes, and make it illegal for them to be accessed from outside the object's methods. In Java it is also considered good practice to write **setters and getters** for all attributes, even if the getter simply retrieves the attribute and the setter just assigns it the value of the parameter which you pass in.

In Python, encapsulation is not enforced by the language, but there is a convention that we can use to indicate that a property is intended to be private and is not part of the object's public interface: we begin its name with an underscore.