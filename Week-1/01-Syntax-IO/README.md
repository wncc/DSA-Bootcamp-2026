# Syntax & I/O - C++, Python, and Java

[Home](../../README.md) > [Week 1](../README.md) > Syntax & I/O

> Week 1 · Topic 1 of 5 · Prerequisites: none

---

## Why This Topic First

You can't think clearly about algorithms when you're distracted by syntax errors. This section is a fast, parallel reference across C++, Python, and Java so the language stops being an obstacle. Read it once, refer back when you need to.

---

## 1. Program Structure

Every C++ program needs a `main()` entry point and headers to access standard library features. Java wraps everything inside a class whose filename must match. Python needs no boilerplate - it runs top to bottom.

**C++**
```cpp
#include <bits/stdc++.h>   // pulls in the entire standard library
using namespace std;        // so you write cout, not std::cout

int main() {
    cout << "Hello, WnCC!" << "\n";
    return 0;
}
```

**Python**
```python
print("Hello, WnCC!")
```

**Java**
```java
public class Main {                          // filename must be Main.java
    public static void main(String[] args) { // OS calls this
        System.out.println("Hello, WnCC!");
    }
}
```

---

## 2. Data Types & Variables

C++ and Java are statically typed - every variable's type is fixed at compile time. Python is dynamically typed - the type is inferred at runtime and can change.

**C++**
```cpp
int a = 10;               // 32-bit integer, up to ~2.1 billion
long long b = 4e18;       // 64-bit - use when values can exceed 2 billion
double d = 3.14159;
char ch = 'A';
bool flag = true;
string name = "WnCC";
```

**Python**
```python
a = 10
b = 4 * 10**18   # Python ints have arbitrary precision - no overflow ever
d = 3.14159
ch = 'A'         # no separate char type; it's just a 1-character string
flag = True
name = "WnCC"
```

**Java**
```java
int a = 10;
long b = 4000000000000000000L;  // suffix L required for long literals
double d = 3.14159;
char ch = 'A';
boolean flag = true;
String name = "WnCC";           // capital S - String is a class, not a primitive
```

### Type Conversion

In C++ and Java, integer division truncates - cast one operand to `double` to get decimals. In Python, `/` always gives a float; use `//` for floor division. The `digit - '0'` trick works in C++ and Java since chars are stored as ASCII values; Python uses `int()`.

**C++**
```cpp
int x = 7, y = 2;
cout << x / y;           // 3 - truncates
cout << (double)x / y;   // 3.5 - cast forces float division

char digit = '7';
int num = digit - '0';   // 7 - '7' is ASCII 55, '0' is 48, difference is 7
```

**Python**
```python
x, y = 7, 2
print(x / y)    # 3.5 - always float
print(x // y)   # 3   - floor division

digit = '7'
num = int(digit)           # 7 - simplest way
num = ord('7') - ord('0')  # 7 - same ASCII trick as C++/Java
```

**Java**
```java
int x = 7, y = 2;
System.out.println(x / y);            // 3 - truncates
System.out.println((double) x / y);   // 3.5

char digit = '7';
int num = digit - '0';                // 7 - same ASCII trick as C++
```

---

## 3. Operators

Arithmetic and comparison operators are identical across all three. Key differences: Python uses `**` for power and `//` for integer division; C++ and Java use `/` between two ints for integer division.

| Operation | C++ | Python | Java |
|---|---|---|---|
| Integer division | `x / y` | `x // y` | `x / y` |
| Power | `pow(x, y)` | `x ** y` | `Math.pow(x, y)` |
| Modulo | `x % y` | `x % y` | `x % y` |

Bitwise operators (`&`, `|`, `^`, `<<`, `>>`) have identical syntax in all three. Two patterns you will use constantly in DSA:

**C++**
```cpp
if (x & 1)   // true if x is odd (any non-zero integer treated as true) - faster than x % 2 == 1
x = x << 1;  // multiply by 2
x = x >> 1;  // integer divide by 2
```

**Java**
```java
if((x & 1) != 0 ) // true if x is odd (no implicit conversion from int to boolean unlike c++)
x = x << 1;  // multiply by 2
x = x >> 1;  // integer divide by 2
```

**Python**
```python
if x & 1:    # odd check
x = x << 1  # multiply by 2
x = x >> 1  # floor divide by 2
```

The ternary operator is a one-liner for simple conditionals:

**C++ and Java**
```cpp
int maxVal = (a > b) ? a : b;
```

**Python**
```python
max_val = a if a > b else b
```

---

## 4. Control Flow

### if / else

Conditions and branching work the same way - Python uses colons and indentation instead of braces, and `elif` instead of `else if`.

**C++**
```cpp
if (score >= 90)      {cout << "A\n";}
else if (score >= 75) {cout << "B\n";}
else                  {cout << "C\n";}
```

**Python**
```python
if score >= 90:    print("A")
elif score >= 75:  print("B")
else:              print("C")
```

**Java**
```java
if (score >= 90)      System.out.println("A");
else if (score >= 75) System.out.println("B");
else                  System.out.println("C");
```

### switch / match

`switch` in C++ and Java jumps directly to the matching case - always add `break` or execution falls into the next case. Python 3.10+ introduced `match` with cleaner syntax and no fall-through issue.

**C++**
```cpp
switch (day) {
    case 1:  cout << "Monday\n";   break;
    case 2:  cout << "Tuesday\n";  break;
    default: cout << "Other\n";    break;
}
```

**Java**
```java
switch (day) {
    case 1:  System.out.println("Monday");   break;
    case 2:  System.out.println("Tuesday");  break;
    default: System.out.println("Other");    break;
}
```

**Python**
```python
match day:
    case 1: print("Monday")
    case 2: print("Tuesday")
    case _: print("Other")
```

---

## 5. Loops

### for

C++ and Java use the classic three-part `for (init; condition; update)`. Python iterates over a `range` object instead.

**C++**
```cpp
for (int i = 0; i < 5; i++) cout << i << " ";
```

**Python**
```python
for i in range(5):          print(i, end=" ")  # 0 1 2 3 4
for i in range(4, -1, -1):  print(i, end=" ")  # 4 3 2 1 0
for i in range(0, 10, 2):   print(i, end=" ")  # 0 2 4 6 8
```

**Java**
```java
for (int i = 0; i < 5; i++) System.out.print(i + " ");
```

### while

Use when the number of iterations is not known in advance.

**C++**
```cpp
int num = 12345;
while (num > 0) {
    cout << num % 10 << " ";  // last digit
    num /= 10;
}
// Output: 5 4 3 2 1
```

**Python**
```python
num = 12345
while num > 0:
    print(num % 10, end=" ")
    num //= 10
```

**Java**
```java
int num = 12345;
while (num > 0) {
    System.out.print(num % 10 + " ");
    num /= 10;
}
```

`break` exits the loop entirely; `continue` skips to the next iteration - syntax is identical across all three.

---

## 6. Functions

Declare return type and parameter types in C++ and Java. Python infers everything. In all three, passing a primitive creates a copy; passing an object/array/list passes a reference to the original.

**C++**
```cpp
int add(int a, int b) { return a + b; }

// Pass vectors by const reference - avoids copying the whole array
void process(const vector<int> &v) { /* v is read-only here */ }
void modify(vector<int> &v) { v[0] = 99; }   // modifies the original
```

**Python**
```python
def add(a, b): return a + b

# Integers and strings are immutable - behave like copies
# Lists and dicts are mutable - modifying them inside changes the original
def double_list(v):
    for i in range(len(v)): v[i] *= 2   # modifies the original list
```

**Java**
```java
static int add(int a, int b) { return a + b; }

// Primitives (int, double, char) are copied - changes don't affect caller
// Arrays and objects are passed by reference - changes affect the original
static void doubleArray(int[] v) {
    for (int i = 0; i < v.length; i++) v[i] *= 2;
}
```

---

## 7. Input & Output

### Reading a Single Value

**C++**
```cpp
int n;
cin >> n;
cout << n << "\n";
```

**Python**
```python
n = int(input())
print(n)
```

**Java**
```java
import java.util.Scanner;
Scanner sc = new Scanner(System.in);
int n = sc.nextInt();
System.out.println(n);
```

### Reading Multiple Values on One Line

**C++**
```cpp
int a, b;
cin >> a >> b;
cout << a + b << "\n";
```

**Python**
```python
a, b = map(int, input().split())
print(a + b)
```

**Java**
```java
int a = sc.nextInt(), b = sc.nextInt();
System.out.println(a + b);
```

### Reading an Array / List

Input: `5` on the first line, then `1 2 3 4 5` on the next.

**C++**
```cpp
int n;
cin >> n;
vector<int> arr(n);
for (int i = 0; i < n; i++) cin >> arr[i];
```

**Python**
```python
n = int(input())
arr = list(map(int, input().split()))
```

**Java**
```java
int n = sc.nextInt();
int[] arr = new int[n];
for (int i = 0; i < n; i++) arr[i] = sc.nextInt();
```

### Reading a String

**C++**
```cpp
string s;
cin >> s;         // single word
getline(cin, s);  // full line (including spaces)
```

**Python**
```python
s = input()                  # always reads a full line
word = input().split()[0]    # first word only
```

**Java**
```java
String word = sc.next();      // single word
String line = sc.nextLine();  // full line
```

### Reading a 2D Grid / Matrix

Input: `3 3`, then 3 rows of 3 integers each.

**C++**
```cpp
int r, c;
cin >> r >> c;
vector<vector<int>> grid(r, vector<int>(c));
for (int i = 0; i < r; i++)
    for (int j = 0; j < c; j++)
        cin >> grid[i][j];
```

**Python**
```python
r, c = map(int, input().split())
grid = [list(map(int, input().split())) for _ in range(r)]
```

**Java**
```java
int r = sc.nextInt(), c = sc.nextInt();
int[][] grid = new int[r][c];
for (int i = 0; i < r; i++)
    for (int j = 0; j < c; j++)
        grid[i][j] = sc.nextInt();
```

---

## Before You Move On

- Can you write a `for` loop in your chosen language without looking it up?
- Can you read an array from stdin and print it back out?
- Can you define a function, pass an array to it, and modify it in-place?

---

## Additional Resources

- **C++:** https://www.geeksforgeeks.org/cpp/c-plus-plus/
- **Python:** https://www.geeksforgeeks.org/python/python-programming-language-tutorial/
- **Java:** https://www.w3schools.com/java/

## Official Documentation

- **C++:** [cppreference.com](https://en.cppreference.com/w/) - the most complete C++ language and standard library reference
- **Python:** [docs.python.org](https://docs.python.org/3/) - official Python 3 documentation, including the tutorial and library reference
- **Java:** [docs.oracle.com/en/java](https://docs.oracle.com/en/java/javase/21/) - official Java SE documentation and API reference

> Learning to read official documentation is a skill in itself - and one of the most valuable habits you can build as a programmer. You won't understand every page at first, but the more you refer to docs instead of just Googling, the faster you'll grow.

---

[Week 1 Overview](../README.md) | [Next: Time & Space Complexity](../02-Complexity/README.md)
