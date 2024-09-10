---
{"dg-publish":true,"permalink":"/1-rough-notes/inheritance-in-c/"}
---


# Inheritance in C++

15-08-2024 15:02

Status: 

Tags: [[3 - Tags/CPP\|CPP]] [[3 - Tags/OOPS\|OOPS]] [[1 - Rough Notes/Virtual in C++\|Virtual in C++]] [[1 - Rough Notes/Access Specifiers and Visibility in C++\|Access Specifiers and Visibility in C++]]


## Types of Inheritance

There are three types of inheritance in C++: public, protected, and private. The type of inheritance affects how the access specifiers of base class members are treated in the derived class.

a) **Public Inheritance:**
   - Public members of the base class become public in the derived class.
   - Protected members of the base class become protected in the derived class.
   - Private members of the base class remain inaccessible in the derived class.

b) **Protected Inheritance:**
   - Public and protected members of the base class become protected in the derived class.
   - Private members of the base class remain inaccessible in the derived class.

c) **Private Inheritance:**
   - Public and protected members of the base class become private in the derived class.
   - Private members of the base class remain inaccessible in the derived class.

## Effects on Access

Let's use an example to illustrate:

```cpp
class Base {
public:
    int a;
protected:
    int b;
private:
    int c;
};

class Derived1 : public Base {};
class Derived2 : protected Base {};
class Derived3 : private Base {};
```

- In Derived1 (public inheritance):
  - 'a' is public
  - 'b' is protected
  - 'c' is inaccessible

- In Derived2 (protected inheritance):
  - 'a' is protected
  - 'b' is protected
  - 'c' is inaccessible

- In Derived3 (private inheritance):
  - 'a' is private
  - 'b' is private
  - 'c' is inaccessible

## Changing Access Specifiers in Derived Class:

You can change the access specifier of inherited members in the derived class, but with some restrictions:

- You can only change the access level of public or protected members from the base class.
- You can only make them more restrictive, not less.

Here's how you can do it:

```cpp
class Base {
public:
    int x;
protected:
    int y;
};

class Derived : public Base {
private:
    using Base::x;  // Make x private in Derived
public:
    using Base::y;  // Make y public in Derived
};
```

In this example:
- 'x', which was public in Base, becomes private in Derived.
- 'y', which was protected in Base, becomes public in Derived.

Important points:
- You cannot change the access level of private members of the base class.
- You cannot make a member less restrictive than it was in the base class.
- This technique uses the 'using' declaration to change access levels.

## Inheriting using `private` or `protected`

### `protected` inheritance
When you inherit using protected inheritance, you can still access the derived class using a pointer of the base class, but only within the inheritance hierarchy. Here's what that means:

- You can use a base class pointer to point to a derived class object within the derived class itself or its further derived classes.
- However, you cannot do this from outside the inheritance hierarchy (e.g., in main() or in unrelated classes).

```cpp
class Base {
public:
    virtual void foo() { cout << "Base::foo()" << endl; }
};

class Derived : protected Base {
public:
    void bar() {
        Base* ptr = this;  // This is allowed
        ptr->foo();  // This works
    }
};

int main() {
    Derived d;
    // Base* ptr = &d;  // This would NOT compile
    // Base* ptr = new Derived // This would not compile either
    // ptr->foo();  // This would NOT compile
    d.bar();  // This works and will call Base::foo()
    return 0;
}
```

```cpp
Base* ptr = &d;  // This would NOT compile
```
The line is trying to treat a `Derived` object (`d`) as if it were a `Base` object (using a pointer). However, because the inheritance is **protected**, you cannot perform this type of conversion outside of the `Derived` class. Protected inheritance restricts access to `Base` through `Derived` outside the class, meaning external code (like in `main`) **does not have access to the fact** that `Derived` is related to `Base`.

### `private` inheritance
When you use private inheritance, all public and protected members of the base class become private members of the derived class. This means:

1. Outside the derived class, you cannot access base class members or use base class pointers/references to refer to derived class objects.
2. Inside the derived class, you can access public and protected members of the base class.
3. Further derived classes cannot access the base class members through this derived class.

This effectively hides the fact that `Derived` is related to `Base` from the outside world.

```cpp
class Base {
public:
    void publicFunction() { cout << "Base::publicFunction()" << endl; }
protected:
    void protectedFunction() { cout << "Base::protectedFunction()" << endl; }
};

class Derived : private Base {
public:
    void derivedFunction() {
        publicFunction();  // OK: Can access Base's public function
        protectedFunction();  // OK: Can access Base's protected function
        
        Base* ptr = this;  // OK: Can use Base pointer inside Derived
        ptr->publicFunction();  // OK: Can call Base's public function through pointer
    }
};

class FurtherDerived : public Derived {
public:
    void furtherDerivedFunction() {
        // publicFunction();  // Error: Can't access Base's function
        // protectedFunction();  // Error: Can't access Base's function
        // Base* ptr = this;  // Error: Can't convert to Base*
    }
};

int main() {
    Derived d;
    // d.publicFunction();  // Error: Can't access Base's function
    // Base* ptr = &d;  // Error: Can't convert Derived* to Base*
    d.derivedFunction();  // OK: This will work and call Base's functions

    FurtherDerived fd;
    // fd.publicFunction();  // Error: Can't access Base's function
    return 0;
}
```
## References