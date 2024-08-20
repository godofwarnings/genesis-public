---
{"dg-publish":true,"permalink":"/1-rough-notes/c-shenanigans/"}
---

# C++ Shenanigans

15-08-2024 16:14

Status: 

Tags: [[3 - Tags/CPP\|CPP]] [[3 - Tags/OOPS\|OOPS]] [[1 - Rough Notes/Classes in C++\|Classes in C++]]

1. Assignment vs Initialization
https://stackoverflow.com/questions/7350155/what-is-the-difference-between-initialization-and-assignment

```cpp
#include <iostream>

class Foo
{
private:
    int m_x{};
    int m_y{};

public:
    Foo(int x, int y)
    {
        m_x = x; // incorrect: this is an assignment, not an initialization
        m_y = y; // incorrect: this is an assignment, not an initialization
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

Although in this simple case this will produce the expected result, in case where members are required to be initialized (such as for data members that are const or references) assignment will not work.

> [!note] Initialization is less costly
> When you initialize fields via initializer list the constructors will be called once. If you use the assignment then the fields will be first initialized with default constructors and then reassigned (via assignment operator) with actual values.

2. In OOPS, why and when one should prefer non-member functions over member functions
https://www.learncpp.com/cpp-tutorial/the-benefits-of-data-hiding-encapsulation/#prefer-non-member-functions

## References