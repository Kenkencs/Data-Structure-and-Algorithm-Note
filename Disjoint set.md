[[Tree]] [[Suffix array]]
# Equivalence Relations

A relation $R$ on a set $S$ is an **equivalence relation** if it satisfies three properties:

1. **Reflexive**: $a \mathrel{R} a$ is true for all $a \in S$.
2. **Symmmetric**: $a \mathrel{R} b \implies b \mathrel{R} a$.
3. **Transitive**: $a \mathrel{R} b$ and $b \mathrel{R} c \implies a \mathrel{R} c$.

> **Key Property**: An equivalence relation divides set $S$ into several **disjoint components** (equivalence classes). Elements in the same component are equivalent to each other.

*💡 Example: The relation "same country" divides the world map into different countries.*

# Equivalence Classes

- **Definition**: The equivalence class of an element $a$ (denoted $[a]$) is the subset of all elements equivalent to $a$.
- **Key Property**: Equivalence classes are **disjoint** (they do not overlap).

> **Example**:
> - Elements: $a, b, c, d$
> - Given: $a \sim b$ and $b \sim c$
> - This creates **two** disjoint equivalence classes:
>   - $[a] = [b] = [c] = \{a, b, c\}$
>   - $[d] = \{d\}$

---
# Array implementation

```
index:  0 1 2 3 4 5
s[]:    0 1 2 3 4 5

Union(1,2)

index:  0 1 2 3 4 5
s[]:    0 1 1 3 4 5

Find(1) = 1
Find(2) = 1
```

*Find = O(1)*
*Union = O(N)*

---
# Tree implementation

1. store up as parent of each node
```txt
	0    1    2    3    4
```
2. Union(1,2)
```txt
	    2
	   /
	  1

	index: 0   1   2   3   4
	A:    -1   2  -1  -1  -1
```

==🔴negative value → root
non-negative value → parent index==

## Follow parents

```txt
       5
      /
     3
    /
   1

A[1] = 3
A[3] = 5
A[5] < 0

Find(1)
1 → 3 → 5
Find(1) = 5
```

>[!note] find(a)= = find(b)
> same root
> same tree
> disjoint set

```txt
sample question
index: 0   1   2   3   4   5
A:    -1   3   3   5  -1  -1

Q1. parent(1) = 3
Q2. parent(3) = 5
Q3. Find(1) = 5
Q4. Find(2) = 5
Q5. 1 and 2 are in the same set
Q6. 4 is separate because A[4] = -1, so 4 is an independent root
```

# Union -by-height

Union-by-height = when merging two trees, put the shorter tree under the taller tree.

```txt
tree a
    1
   /
  2

tree b
      5
     /
    6
   /
  7
  
      5
     / \
    6   1
   /     \
  7       2

old height of B = 2
new height      = 2
```

>different heights:
>new height = larger old height
>
>same heights:
>new height = old height + 1

==🔴lower-> higher, height no change!!!==

# Union by size ->path compression 

O(log n)

```cpp
int Find(int element)
{
    if (A[element] < 0)
        return element;
    else
        return A[element] = Find(A[element]);
}
```

---
# Application -> maze generation

```cpp
while entrance and exit are not connected:
    randomly choose a wall between adjacent cells i and j

    if Find(i) != Find(j):
        Union(i,j)
        remove the wall
```

```txt
different roots
→ not connected
→ safe to connect

same root
→ already connected
→ don't break wall
```
