# Pointers
```cpp
class MyClass {
public:
    int firstNum;
    int secondNum;

    int GetSum() {
        int sum = firstNum + secondNum;
        return sum;
    }
}
```
## Raw Pointers
```cpp
void foo() {
    // Manually new a pointer
    MyClass* myClassPtr = new MyClass();

    // Do stuff with myClassPtr
    myClassPtr->firstNum = 1;
    myClassPtr->secondNum = 2;

    // Done with myClassPtr, manually delete it.
    // Otherwise when run out of the scope of function foo
    // the memory space of myClassPtr can never be recycled (deleted)
    // This is called "Memory leak"
    delete myClassPtr;
}
```
## Shared Pointers
```cpp
void foo() {
    // No need to new, just plain declaration
    // SharedPtr class will automatically call `new MyClass()` under the hood
    SharedPtr<MyClass> myClassSharedPtr;

    // Do stuff with myClassPtr
    myClassSharedPtr->firstNum = 1;
    myClassSharedPtr->secondNum = 2;

    // Done with myClassSharedPtr, need to do nothing
    // SharedPtr class will automatically delete the underlying MyClass object
    // when itself runs out of function scope
}
```
# Templates
```cpp
template <typename T> class MyClass {
public:
    T first;
    T second;

    T GetSum() {
        T sum = first + second;
        return sum;
    }
}
```
## Using different types in template
```cpp
// int as template
MyClass<int> myIntClass = new MyClass<int>();
myIntClass->first = 1;
myIntClass->second = 2;
int intSum = myIntClass->GetSum(); // intSum = 3

// double as template
MyClass<double> myDoubleClass = new MyClass<double>();
myDoubleClass->first = 3.14;
myDoubleClass->second = 5.12;
double doubleSum = myDoubleClass->GetSum(); // doubleSum = 8.26

// string as template
MyClass<string> myStrClass = new MyClass<string>();
myStrClass->first = "1";
myStrClass->second = "2";
string strSum = myStrClass->GetSum(); // strSum = "12"
```

## SharedPtr class is also a template
```cpp
// Example of a combination of all above: Recursive (nested) template arguments
// SharedPtr calls `new MyClass<string>` automatically under the hood
SharedPtr<MyClass<string>> mySharedStrClass;

mySharedStrClass->first = "hello, ";
mySharedStrClass->second = "world";
string strSum = mySharedStrClass->GetSum(); // strSum = "hello, world"
```

