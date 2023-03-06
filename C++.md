## Table of Contents  

<a href="https://stackoverflow.com/a/4757718/7277094">Forward Declaration</a><br/>
<a href="https://learn.microsoft.com/en-us/cpp/cpp/namespaces-cpp?view=msvc-170">Namespaces</a><br/>
<a href="#smart-pointers-1">Smart Pointers</a><br/>
<a href="#reference-variables-1">Reference Variables</a><br/>
<a href="#memory-model-1">Memory Model</a><br/>
<a href="#footnotes">footnotes</a><br/>

## Smart Pointers [^1]
### Pointers
In C++, a normal pointer is a variable that holds the memory address of another object. It is created using the * operator, and it can be dereferenced using the * operator to access the object it points to. Normal pointers are commonly used in C++ for dynamic memory allocation and for passing objects to functions by reference.

Here's an example of using a normal pointer:

```
#include <iostream>

int main() {
    int* ptr = new int(42);
    std::cout << *ptr << std::endl; // prints 42
    delete ptr;
    return 0;
}
```
In this example, we use the new operator to dynamically allocate an int on the heap, and we assign its address to a normal pointer named ptr. We then dereference ptr to access the value of the int, and we delete it using the delete operator to avoid a memory leak.
### Caveats of using pointers
One caveat of using normal pointers is that they do not manage the lifetime of the object they point to automatically. It is the programmer's responsibility to ensure that the object is properly deleted when it is no longer needed. Forgetting to delete an object can result in a memory leak, where the memory allocated for the object is never reclaimed by the system. Additionally, deleting an object twice can result in undefined behavior, where the program crashes or behaves unpredictably.

Another caveat of using normal pointers is that they can be null, meaning that they do not point to a valid object. Dereferencing a null pointer results in undefined behavior, where the program crashes or behaves unpredictably. To avoid this, it is a good practice to initialize pointers to null and to check for null before dereferencing them.
```
#include <iostream>

int main() {
    int* ptr = nullptr;
    if (ptr != nullptr) {
        std::cout << *ptr << std::endl;
    }
    return 0;
}
```
In this example, we initialize the ptr pointer to null, and we check for null before dereferencing it to avoid undefined behavior.
### Need of smart pointers
Overall, while normal pointers are a powerful tool in C++, they require careful management and can be error-prone. Smart pointers provide an alternative that automates memory management and helps prevent common mistakes. Smart pointers are objects that behave like pointers, but they automatically manage the lifetime of the object they point to. They ensure that the memory allocated for the object is properly deallocated when it is no longer needed, even in the presence of exceptions or early returns. In other words, smart pointers provide an automatic way of managing memory, so you don't have to worry about explicitly deleting objects or accidentally deleting them too soon.
### Types of smart pointers
There are several types of smart pointers in C++, each with its own unique behavior and use case. Here are the most common ones:

1. `unique_ptr`: This type of smart pointer represents an exclusive ownership of a dynamically allocated object. It cannot be copied, only moved. When the unique_ptr goes out of scope or is explicitly reset, it automatically deletes the object it owns. Here's an example:
```
#include <memory>
#include <iostream>

int main() {
    std::unique_ptr<int> ptr(new int(42));
    std::cout << *ptr << std::endl; // prints 42
    *ptr = 84;
    std::cout << *ptr << std::endl; // prints 84
    return 0;
} // ptr automatically deletes the int it owns
```
2. `shared_ptr`: This type of smart pointer represents shared ownership of a dynamically allocated object. It keeps track of the number of shared_ptr objects that point to the same object, and when the last one goes out of scope or is explicitly reset, it deletes the object. Here's an example:
```
#include <memory>
#include <iostream>

int main() {
    std::shared_ptr<int> ptr1(new int(42));
    std::shared_ptr<int> ptr2 = ptr1;
    std::cout << *ptr1 << std::endl; // prints 42
    std::cout << *ptr2 << std::endl; // prints 42
    *ptr1 = 84;
    std::cout << *ptr2 << std::endl; // prints 84
    return 0;
} // ptr1 and ptr2 both delete the int they share ownership of
```
3. `weak_ptr`: This type of smart pointer represents weak ownership of a dynamically allocated object. It is used in conjunction with shared_ptr to avoid circular references that can cause memory leaks. It can be used to check if the object it points to still exists without actually owning it. Here's an example:
```
#include <memory>
#include <iostream>

int main() {
    std::shared_ptr<int> ptr1(new int(42));
    std::weak_ptr<int> ptr2 = ptr1;
    std::cout << *ptr1 << std::endl; // prints 42
    std::cout << *ptr2.lock() << std::endl; // prints 42
    ptr1.reset();
    if (ptr2.expired()) {
        std::cout << "ptr1 is gone" << std::endl;
    }
    return 0;
} // ptr2 does not delete the int it weakly owns
```
The need for smart pointers arises from the fact that C++ does not have garbage collection
    

## Reference variables [^1]
### What are variables in C++?
Variables are named memory locations that hold values of a specific type in a C++ program. In order to use variables in our program, we need to declare them first.

Here's an example:
```
int my_variable;
```
This declares a variable named my_variable of type int.

We can also initialize the variable with a value:

```
int my_variable = 42;
```
### What is a reference in C++?
A reference is an alias for an existing variable. It allows us to refer to the variable by a different name. When we use a reference, we're not creating a new variable – we're simply creating a new name for an existing variable.

Here's an example:
```
int my_variable = 42;
int& my_reference = my_variable;
```
This creates a reference named my_reference that refers to the variable my_variable. Now, we can use my_reference in place of my_variable:
```
my_reference = 69;
std::cout << my_variable << std::endl; // Output: 69
```
Note that when we assign a value to my_reference, we're actually changing the value of my_variable, because they refer to the same memory location.

### How to declare a reference in C++?
We declare a reference by using the & symbol after the variable type:
```
int my_variable = 42;
int& my_reference = my_variable;
```
Here, my_reference is declared as a reference to an integer (int&).

### When to use references in C++?
References are useful when we want to pass variables to functions or methods without copying them. This can be more efficient than passing variables by value, especially for large data types like arrays or objects.

For example:
```
void increment(int& n) {
    n++;
}

int main() {
    int my_variable = 42;
    increment(my_variable);
    std::cout << my_variable << std::endl; // Output: 43
    return 0;
}
```
Here, we're passing my_variable to the increment() function by reference. When we modify the value of n inside the function, we're actually modifying the value of my_variable.

### How to use references with pointers in C++?
Pointers and references are related in C++. We can use the dereference operator (*) with a pointer to access the value it points to, and we can use the address-of operator (&) with a reference to get the memory address of the variable it refers to.

For example:

```
int my_variable = 42;
int* my_pointer = &my_variable; // Pointer to my_variable
int& my_reference = *my_pointer; // Reference to the value pointed to by my_pointer

my_reference = 69;
std::cout << my_variable << std::endl; // Output: 69
std::cout << *my_pointer << std::endl; // Output: 69
```
Here, we're creating a pointer named my_pointer that points to my_variable. We're then creating a reference named my_reference that refers to the value pointed to by my_pointer. When we modify the value of my_reference, we're actually modifying the value of my_variable.

### What are const references in C++?
A const reference is a reference that can't be used to modify the value it refers to. It's useful for passing variables to functions without allowing the function to modify them.

For example:

```
void print(const int& n) {
    std::cout << n << std::endl;
```
## Memory Model [^1]
C++ is a programming language that provides a lot of flexibility when it comes to managing memory. Understanding the C++ memory model and lifetime of objects is crucial for writing efficient and robust programs.

The memory model of a programming language defines how the memory is organized and accessed by the programs. In C++, the memory model is divided into two types of storage:

1. **Stack**: The stack is a region of memory where variables and objects with automatic storage duration are allocated. The stack is a last-in, first-out (LIFO) data structure, which means that the most recently added item is the first to be removed.

2. **Heap**: The heap is a region of memory where objects with dynamic storage duration are allocated. Unlike the stack, the heap is not managed automatically by the compiler. Instead, the programmer must explicitly request memory allocation and deallocation.

### Lifetime of Objects
The lifetime of an object in C++ is the period of time during which the object exists in memory. The lifetime of an object depends on its storage duration, which can be one of the following:

1. **Static storage duration**: Objects with static storage duration are allocated at the start of the program and exist until the program terminates. Examples include global variables and static class members.

2. **Thread storage duration**: Objects with thread storage duration are allocated for each thread and exist until the thread terminates. Examples include thread-local variables.

3. **Automatic storage duration**: Objects with automatic storage duration are allocated on the stack when a function is called and exist until the function returns. Examples include local variables.

4. **Dynamic storage duration**: Objects with dynamic storage duration are allocated on the heap and exist until they are explicitly deallocated. Examples include objects created with the new operator.

### Stack vs Heap
Stack allocation is faster than heap allocation because the stack is managed by the compiler, and the allocation and deallocation of stack memory are done automatically. However, the stack is limited in size, and the size of the objects allocated on the stack must be known at compile time.

Heap allocation is slower than stack allocation because the allocation and deallocation of heap memory must be done manually by the programmer. However, the heap is not limited in size, and objects allocated on the heap can be resized dynamically at runtime.

In general, you should use stack allocation for small objects with known sizes and lifetimes that are short and predictable, such as local variables in functions. You should use heap allocation for large objects or objects with unknown sizes and lifetimes that are long and unpredictable, such as objects created dynamically during runtime.

Here is an example to demonstrate the use of stack and heap memory:

```
#include <iostream>

using namespace std;

class MyClass {
public:
    MyClass() { cout << "Constructor called" << endl; }
    ~MyClass() { cout << "Destructor called" << endl; }
};

void foo() {
    MyClass obj;  // object allocated on the stack
}

int main() {
    foo();  // object allocated on the stack is created and destroyed
    MyClass* ptr = new MyClass();  // object allocated on the heap
    delete ptr;  // object allocated on the heap is destroyed
    return 0;
}
```
In the above example, the MyClass object created in the foo() function is allocated on the stack and has automatic storage duration. When the foo() function returns, the object is automatically deallocated.

The MyClass object created with the new operator in the main() function is allocated on the heap and has dynamic storage duration. The delete operator is used to explicitly deallocate the object.

In conclusion, understanding the C++ memory model and lifetime of objects is important for writing efficient and robust programs.
## Footnotes
[^1]: Generated by ChatGPT.
