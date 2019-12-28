# Pengzh Best Practices

## Resources

[Bjarne Stroustrup's C++ Style and Technique FAQ](http://www.stroustrup.com/bs_faq2.html)

## Basic Rules

1. Use `nullptr`
2. Always use namespace. Never use `using namespace` in a header file.

## Parameters: in, out, in-out

### For “in” parameters, pass cheaply-copied types by value and others by reference to const

```cpp
void f1(const string& s);  // OK: pass by reference to const; always cheap

void f2(string s);         // bad: potentially expensive

void f3(int x);            // OK: Unbeatable

void f4(const int& x);     // bad: overhead on access in f4()
```

### Work with HRESULT

```cpp
HRESULT input(const string& inputString, int inputNum);

HRESULT output(string& outputString, int& outputNum);
```

## Function const

### When a function is declared as const, it can be called on any type of object. Non-const functions can only be called by non-const objects.

```cpp
class Test { 
    int value; 
public: 
    Test(int v = 0) {value = v;} 
      
    // We get compiler error if we add a line like "value = 100;" 
    // in this function. 
    int getValue() const {return value;}   
}; 
  
int main() { 
    Test t(20); 
    cout<<t.getValue(); 
    return 0; 
} 
```

## unique_ptr vs shared_ptr

1. Use unique_ptr when you want a single pointer to an object that will be reclaimed when that single pointer is destroyed.
2. Use shared_ptr when you want multiple pointers to the same resource.

```cpp
unique_ptr<T> myPtr(new T);       // Okay
unique_ptr<T> myOtherPtr = myPtr; // Error: Can't copy unique_ptr
unique_ptr<T> myOtherPtr = std::move(myPtr); // Okay, resource now stored in myOtherPtr

shared_ptr<T> myPtr(new T);       // Okay
shared_ptr<T> myOtherPtr = myPtr; // Sure!  Now have two pointers to the resource.
```