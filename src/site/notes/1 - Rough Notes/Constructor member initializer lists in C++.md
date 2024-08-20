---
{"dg-publish":true,"permalink":"/1-rough-notes/constructor-member-initializer-lists-in-c/"}
---

# Constructor member initializer lists in C++

15-08-2024 15:51

Status: 

Tags: [[3 - Tags/CPP\|CPP]] [[3 - Tags/OOPS\|OOPS]]

## Member initializer lists

To have a constructor initialize members, we do so using a **member initializer list** (often called a “member initialization list”). Do not confuse this with the similarly named “initializer list” that is used to initialize aggregates with a list of values.

- The member initializer list is defined after the constructor parameters. It begins with a colon (:), and then lists each member to initialize along with the initialization value for that variable, separated by a comma. 
- You must use a direct form of initialization here (preferably using braces, but parentheses works as well) -- using copy initialization (with an equals) does not work here. 
- Also note that the member initializer list does not end in a semicolon.
- This is the recommended style
```cpp
Foo(int x, int y)
    : m_x { x }
    , m_y { y }
{
}
```

### Order of initialization
- Because the C++ standard says so, the members in a member initializer list are always initialized in the order in which **they are defined inside the class** (not in the order they are defined in the member initializer list).
- In the above example, if `m_x` is defined before `m_y` in the class definition, `m_x` will be initialized first (even if it is not listed first in the member initializer list).
```cpp
#include <algorithm> // for std::max
#include <iostream>

class Foo
{
private:
    int m_x{};
    int m_y{};

public:
    Foo(int x, int y)
        : m_y{ std::max(x, y) }, m_x{ m_y } // issue on this line
    {
    }

    void print() const
    {
        std::cout << "Foo(" << m_x << ", " << m_y << ")\n";
    }
};

int main()
{
    Foo foo{ 6, 7 };
    foo.print();

    return 0;
}
```
OUTPUT
```js
Foo(-858993460, 7)
```
Even though `m_y` is listed first in the member initialization list, because `m_x` is defined first in the class, `m_x` gets initialized first. And `m_x` gets initialized to the value of `m_y`, which hasn’t been initialized yet. Finally, `m_y` gets initialized to the greater of the initialization values.

> [!note] Good Practice
> Member variables in a member initializer list should be listed in order that they are defined in the class.

### Member initializer list vs default member initializers
If a member has both a default member initializer and is listed in the member initializer list for the constructor, the member initializer list value takes precedence.
```cpp
#include <iostream>

class Foo
{
private:
    int m_x{};    // default member initializer (will be ignored)
    int m_y{ 2 }; // default member initializer (will be used)
    int m_z;      // no initializer

public:
    Foo(int x)
        : m_x{ x } // member initializer list
    {
        std::cout << "Foo constructed\n";
    }

    void print() const
    {
        std::cout << "Foo(" << m_x << ", " << m_y << ", " << m_z << ")\n";
    }
};

int main()
{
    Foo foo{ 6 };
    foo.print();

    return 0;
}
```
OUTPUT
```js
Foo constructed
Foo(6, 2, -858993460)
```
`m_z` will have undefined behavior since it is uninitialized. 

> [!warning] You will have (rather forced) to use a Member Initializer list if:
> - Your class has a reference member  
> - Your class has a const member or
> - If the base class does not have a default constructer.
## References