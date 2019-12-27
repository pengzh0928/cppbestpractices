# Pengzh Best Practices

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