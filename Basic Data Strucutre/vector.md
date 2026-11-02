# Vector
[[Data Structure]]

## What is it?

A dynamic array in C++.

---

## When should I use it?

- Need dynamic size
- Random access by index
- Frequent insertion at the end (`push_back()`)

---

## Ways to create a vector

```cpp
vector<int> v1;
```

Empty vector.

```cpp
vector<int> v2(5);
```

Size = 5, all values are `0`.

```cpp
vector<int> v3(5, 10);
```

Size = 5, all values are `10`.

```cpp
vector<int> v4 = {1,2,3};
```

Initialize with existing values.

---

## Adding Elements ⭐⭐⭐⭐⭐

### Add a new element

```cpp
v.push_back(10);
```

Before:

```
[]
```

After:

```
[10]
```

---

### Modify an existing element

```cpp
v[0] = 10;
```

Works **only if index 0 already exists**.

Example:

```cpp
vector<int> v(3);

v[0] = 10;
```

Result:

```
[10,0,0]
```

---

## Common Beginner Mistakes ⭐⭐⭐⭐⭐

❌

```cpp
vector<int> v;

v[0] = 5;
```

Reason:

The vector is empty.

Index 0 doesn't exist.

✅

```cpp
v.push_back(5);
```

---

## STL

push_back() O(1)

pop_back()  delete end

pop_front() delete front

size()

empty()

clear()

resize()

begin()

end()

.size()

.erase()

---

## Complexity

Access          O(1)

push_back()     O(1) amortized

Insert Middle   O(n)

Erase Middle    O(n)

---

## 2D vector
```cpp
vector<vector<int>> mat; 
```
创建一个二维数组

当然可以创建n个row 然后push.back 回去，但不方便

```cpp
vector<vector<int>> table(3, vector<int>(4, 0));
    // 给表格赋值：第 2 行（下标1） 第 3 列（下标2） 赋值为 99
    table[1][2] = 99;
```
直接在vector里面创造数组的大小，行，里面的是列

当然也可以直接赋值
```cpp
vector<vector<int>> table = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };
```
*不一定row 里面相同大小*


---









