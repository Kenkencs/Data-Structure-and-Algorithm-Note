[[Tree]] [[Disjoint set]]
后缀数组
？

> method of fast string searching

a substring that starts at some position and continues all the way to the end
S[T] , where  1$\leq$ i $\leq$ n

```txt
T = ABCAB

S[1] = ABCAB
S[2] = BCAB
S[3] = CAB
S[4] = AB
S[5] = B
```

# Sort suffixes first

```txt
AB     starts at 4
ABCAB  starts at 1
B      starts at 5
BCAB   starts at 2
CAB    starts at 3

Suffix Array = [4, 1, 5, 2, 3]
```

- all suffixes beginning with the same pattern
- appear next to each other

```txt
if 
T = ABCAB
P = AB
return AB , ABCAB 
```
>lower bound → first suffix starting with ANA
>upper bound → position after the last suffix starting with ANA

==🔴Binary search ->O(P log T)==


| QSort , comparison sort | Radix sort | Doubling    | Skew |
| ----------------------- | ---------- | ----------- | ---- |
| O($n^2 \log n$)         | O($n^2$)   | O($\log n$) | O(n) |

# Doubling Algorithm

>用人话说，就是每次将suffix向后延长1，2，4，6，8... 来比较

```txt
T = banana

a... < b... < n...

banana
anana
nana
ana
na
a

at l = 1

banana → b
anana  → a
nana   → n
ana    → a
na     → n
a      → a

at l = 2
anana → an
ana   → an
a     → a

a < an
an = an

```
每次都向后延长，每次来比较，直到超过l的长度

>Compare first L chars.
>
>If different:
    done.
>
>If equal:
    compare the next L chars.

>[!tips]
>if S[i] <L S[j]
→ S[i] <2L S[j]

> [!tips] 
> if S[i] =L S[j]
→ compare S[i+L] and S[j+L]


---
# Suffix tree
>


