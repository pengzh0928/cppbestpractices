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