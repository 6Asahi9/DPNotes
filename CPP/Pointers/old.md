Got you — **clean, small, no over-explanation, pure revision on ONLY old (raw) pointers.**
I’ll just show **allowed vs not allowed** in two parts: **(A) normal stuff** and **(B) OOP stuff.**

---

# 🔷 **A) OLD POINTERS — NORMAL STUFF**

## ✅ Allowed

```cpp
int x = 10;
int* p = &x;      // pointer to stack variable
```

```cpp
int* p = new int(5);   // heap allocation
```

```cpp
int* p = new int(5);
int* q = p;            // two pointers to same heap memory
```

```cpp
int x = 10;
int* p = &x;
*p = 20;               // modifies x
```

```cpp
int* p = new int(5);
delete p;              // free heap memory
p = nullptr;           // good practice
```

```cpp
int* p = nullptr;      // valid null pointer
```

```cpp
int x = 10;
int* p = nullptr;
p = &x;                // later assignment
```

```cpp
int x = 10;
int* p = &x;
int** z = &p;          // pointer to a pointer
```

---

## ❌ NOT Allowed (compile errors)

```cpp
int x = 10;
int* p = x;    // ❌ type mismatch (int vs int*)
```

```cpp
int* p = 10;   // ❌ random address, invalid
```

```cpp
int x = 10;
delete &x;     // ❌ deleting stack memory
```

```cpp
int* p;        // uninitialized
*p = 5;        // ❌ undefined behavior (dangling)
```

```cpp
int* p = new int(5);
int* q = &p;   // ❌ types mismatch (int** vs int*)
```

---

# 🔷 **B) OLD POINTERS — WITH OOP (CLASSES)**

## ✅ Allowed

```cpp
struct Cat {
    int age;
};

Cat c;
Cat* p = &c;          // pointer to stack object
```

```cpp
Cat* p = new Cat();   // heap object
```

```cpp
Cat* p = new Cat();
p->age = 3;           // arrow operator works
```

```cpp
Cat* p = new Cat();
delete p;             // valid
p = nullptr;
```

```cpp
Cat* p = nullptr;
p = new Cat();        // later assignment
```

```cpp
Cat* p = new Cat();
Cat* q = p;           // two pointers to same object
```

---

## ❌ NOT Allowed (compile errors / UB)

```cpp
Cat c;
delete &c;        // ❌ cannot delete stack object
```

```cpp
Cat* p;           // uninitialized
p->age = 3;       // ❌ UB (dangling)
```

```cpp
Cat* p = new Cat();
Cat* q = &p;      // ❌ type mismatch (Cat** vs Cat*)
```

```cpp
Cat* p = new Cat();
delete p;
p->age = 5;       // ❌ UB (use-after-free)
```

```cpp
Cat c;
Cat* p = c;       // ❌ type mismatch (Cat vs Cat*)
```

---

# Tiny memory rules to keep in your head (revision cheats)

* `&x` → address of **stack** variable
* `new` → allocates **heap** memory
* `delete` → destroys **heap memory only**
* Multiple raw pointers can point to same heap → **no tracking, your responsibility**
* Dangling pointer = pointer to memory that is already deleted → **UB**

---

If you want, next I can do the same kind of **clean revision but ONLY for smart pointers** (same style: allowed vs not allowed).
