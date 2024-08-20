---
{"dg-publish":true,"permalink":"/1-rough-notes/access-specifiers-and-visibility-in-c/"}
---

# Access Specifiers and Visibility in C++

15-08-2024 00:35

Status: 

Tags: [[3 - Tags/CPP\|CPP]] [[3 - Tags/OOPS\|OOPS]] [[Polymorphism\|Polymorphism]] [[1 - Rough Notes/Virtual in C++\|Virtual in C++]] [[1 - Rough Notes/Inheritance in C++\|Inheritance in C++]]

## Access Specifier
- `private`: Only accessible within the same class
- `protected`: Accessible within the same class and derived classes
- `public`: Accessible from anywhere

## A derived class can change the access specifier of a function it's overriding

This is a feature in C++ that allows derived classes to modify the accessibility of inherited members. Here's a more detailed explanation:

- You can make a base class's protected members public or private; or a base's public members protected or private. You cannot, however, make a base's private members public or protected.

- Rationale: This feature allows derived classes to adapt the interface they present to their users, which can be useful for encapsulation and design purposes.

- Example:
  ```cpp
  class Base {
  public:
      virtual void foo() {}
  };

  class Derived : public Base {
  private:
      void foo() override {}  // Legal: public -> private
  };
  ```

- Implications: This can lead to situations where a function is callable through a base class pointer but not directly on a derived class object.

2. Important concept - Access vs. Visibility:

This distinction is crucial for understanding how virtual functions and inheritance interact with access control in C++:

- Access: Refers to the ability to directly call or use a member from a given context. It's determined by access specifiers (`public`, `protected`, `private`).
  - Example: A `private` member can only be accessed within its own class.

- Visibility: In the context of virtual functions, refers to whether a function participates in dynamic dispatch (virtual function call resolution).
  - A function that overrides a virtual function is always visible to the virtual dispatch mechanism, regardless of its access specifier.

- Key point: Access control is checked at compile-time based on the static type of the expression used to access the member. Virtual function dispatch happens at runtime based on the dynamic type of the object.

- Example:
  ```cpp
  class Base {
  public:
      virtual void foo() { cout << "Base" << endl; }
  };

  class Derived : public Base {
  private:
      void foo() override { cout << "Derived" << endl; }
  };

  int main() {
      Base* b = new Derived();
      b->foo();  // Calls Derived::foo() despite it being private
      // Derived d;
      // d.foo();  // This would be a compile error
  }
  ```

- Implications: 
  1. A `private` override in a derived class can still be called through a base class pointer.
  2. This can lead to a situation where a method is callable on an object in some contexts but not others, which might be counter-intuitive.

Understanding these concepts is crucial for mastering C++ inheritance and polymorphism, as they highlight the subtle interplay between access control and virtual function mechanics in the language.


## References