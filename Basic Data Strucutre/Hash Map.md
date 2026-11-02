# Hash Map

[[vector]] 

## What is it?

using hash map , the key will compare with the value 

*hash function*

time complexity : O(1) , worse O(n)

---
## Why should I use it 

Replace repeated linear searches with average O(1) lookups after building the hash table.

**无序 + 精确查找 + 数据量大 + 不在乎内存** → 用 `unordered_map`。  
**其余情况（有序、范围查、小数据、内存紧）** → 优先考虑 `map` 或 `vector`。

---
## Method to create hash map

```cpp
#include <unordered_map>
```
 must include the header

```cpp
unordered_map<key, value> classname;
```
create the hash map

```cpp
auto pair : mp
```
copy a hash map from mp , then we can have operation


```cpp
mp.find(num) 
```
find the number in the hash map


```cpp
mp.end()
```
the last index in the hash map

```cpp
if(mp.find(num)!=mp.end())
```
which mean that the number is not at the final line,**找这个数字，找到的位置不是终点线（`end`）** , which mean that we got the answer in the hash map

```cpp
{mp[num[i]],i}
```
num`[i]` is the index of num`[i]` in the hash map

---
## Compare
|数据结构|存储 26 个小写字母计数|额外带的“垃圾”|
|---|---|---|
|**数组（vector）**|**~128 字节**|几乎没有|
|**哈希表（unordered_map）**|**~600 字节**|指针、节点头、桶数组、内存管理器标记|

**如果数据范围很小且已知**（比如 26 个小写字母、128 个 ASCII 码、1万个学号）：**无脑用数组（vector/array）**，又快又省。

**如果数据范围极大或不确定**（比如存全世界所有人的身份证号，范围是 0 ~ 10^18）：这时候开数组会瞬间爆内存，必须用 `unordered_map`（只存出现过的）

---
当你调用 `unordered_map.find(key)` 时，底层发生了这三步：

1. **计算哈希值（Hash Function）**：调用哈希函数 `hash(key)`，将任意长度的 Key 映射为一个整数（如 `size_t`）。
    
2. **取模映射（Modulo Operation）**：用这个哈希值 对 桶数组的大小（`bucket_count`）取模，得到桶的索引：`index = hash(key) % bucket_count`。
    
3. **内存寻址**：直接通过 `index` 访问数组中的那个“桶（Bucket）”。
    

**为什么快？** 步骤 1 和 2 都是简单的数学运算（整数运算），步骤 3 是内存直接寻址。**这三个步骤都不需要遍历容器中的元素数量**，因此与元素总数 `n` 无关，所以是 **O(1)**。

### 为什么是“平均”O(1)？（负载因子与冲突）

虽然直接跳到了下标，但不同的 Key 可能算出相同的下标（这叫**哈希冲突**，比如 `hash("ab") % 10` 和 `hash("ba") % 10` 可能相等）。

- **解决冲突**：C++ 的 `unordered_map` 采用**链地址法**，每个桶里挂着一个链表（或红黑树）。
    
- **平均情况**：C++ 标准库通过 **负载因子（Load Factor）** 控制，默认负载因子为 1.0。这意味着桶的数量总是大于等于元素数量。通过自动扩容（Rehash），**保证每个桶里平均只有 1 个元素**。所以即使发生冲突，链表极短，遍历链表的时间也是常数（O(1)）。
    
- **均摊（Amortized）**：扩容时重新哈希（Rehash）会耗费 O(n) 时间，但因为扩容次数很少，把这次成本分摊到每一次插入中，**均摊下来依然是 O(1)**。

---
# Hash functions

**using prime factor**

h(k)=(2k+3)mod11

| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 11  | 15  | 16  |     |     | 12  |     |     | 8   |     | 20  |
有collision就linear search

# Collision Resoluation

1. linear probing 
	1. slot_id +1 , +2....
2. Quadratic probing
	1. slot_id +1^2
3. separate chaining
	1. linked list for the data
4. Double hashing
	   优先跟一开始的hash function then 算h2的hash function，以他为步长
	   ie：slot_id + i * slot_id2 
	   
