---
tags: [basic, complexity]
created: 2026-06-17
status: 🟡
---

# 時間複雜度 & 空間複雜度

## 一句話說明
時間複雜度 = 程式跑多快，空間複雜度 = 程式吃多少記憶體。  
**分析它們是為了能在寫 code 前就知道這個解法會不會太慢、會不會爆記憶體。**

---

## 什麼是時間複雜度 —— Big O 記號

Big O 描述的是：**當輸入 n 很大很大時，執行時間的增長趨勢**。

不是精確秒數，而是「n 變兩倍，時間會變幾倍？」

| Big O | 名稱 | 成長速度 | n=10 | n=100 | n=1000 |
|-------|------|---------|------|-------|--------|
| O(1) | 常數 | 不隨 n 變 | 1 | 1 | 1 |
| O(log n) | 對數 | 很慢 | ~3 | ~7 | ~10 |
| O(n) | 線性 | 成正比 | 10 | 100 | 1000 |
| O(n log n) | 線性對數 | 稍快 | ~33 | ~700 | ~10000 |
| O(n²) | 平方 | 很快 | 100 | 10000 | 1e6 |
| O(2ⁿ) | 指數 | 爆炸 | 1024 | 1e30 | — |

**關鍵直覺**：
- O(1)：陣列索引 `arr[i]`
- O(n)：一層 for 迴圈
- O(n²)：兩層 for 迴圈
- O(log n)：二分搜尋
- O(n log n)：Merge Sort

---

## 如何分析時間複雜度

### 步驟一：找到 n 是什麼

n 通常是陣列長度、字串長度、tree 的節點數。

```cpp
vector<int> arr = {1, 2, 3, ..., n};  // 這裡的 n = arr.size()
```

### 步驟二：數迴圈層數

```cpp
// O(n) —— 一層 for
for (int i = 0; i < n; i++) { ... }

// O(n²) —— 兩層 for
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) { ... }
}

// O(n²) —— 雖然 j 從 i 開始，但大約是 n²/2 → 還是 O(n²)
for (int i = 0; i < n; i++) {
    for (int j = i; j < n; j++) { ... }
}
```

### 步驟三：遞迴看 call tree

```cpp
// Merge Sort：每次切成兩半，總共 log n 層，每層合併 O(n)
// → O(n log n)

// Fibonacci 樸素版：每個呼叫分出兩個，深度 n
// → O(2ⁿ) 超級慢！！！
int fib(int n) {
    if (n <= 1) return n;
    return fib(n-1) + fib(n-2);
}
```

### 步驟四：加法取最大，乘法照算

```cpp
// O(n) + O(n²) → O(n²)  （只取最大的）
for (int i = 0; i < n; i++) { ... }        // O(n)
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) { ... }    // O(n²)
}

// O(n) * O(n) → O(n²)
for (int i = 0; i < n; i++) {              // 外層
    // O(n) 的操作                        // 內層
}
```

---

## 什麼是空間複雜度

除了輸入資料本身之外，你的程式**額外**用了多少記憶體。

```cpp
// O(1) —— 只用了幾個變數
void selectionSort(vector<int>& arr) {
    int n = arr.size();
    int minIdx;  // 就這個
    // ...
}

// O(n) —— 額外開了一個跟 arr 一樣大的陣列
void merge(vector<int>& arr, int l, int m, int r) {
    vector<int> temp(r - l + 1);  // 額外 O(n) 空間
    // ...
}

// O(n) —— 遞迴深度 n（每個 call 在 stack 上佔空間）
void recursion(int n) {
    if (n == 0) return;
    recursion(n - 1);
}
```

**常見的空間複雜度**：

| 空間 | 發生情況 |
|-----|---------|
| O(1) | 只用了幾個變數（in-place） |
| O(n) | 開了跟輸入一樣大的陣列 / map / set |
| O(n²) | 開了 n×n 的二維陣列 |
| O(n) | 遞迴深度 n（merge sort 遞迴深度 log n → O(log n)） |

---

## 分析實戰 —— 以排序為例

| 排序 | 時間（平均） | 時間（最壞） | 空間 | 原因 |
|-----|-------------|-------------|------|------|
| Bubble Sort | O(n²) | O(n²) | O(1) | 兩層 for，in-place |
| Selection Sort | O(n²) | O(n²) | O(1) | 兩層 for，in-place |
| Insertion Sort | O(n²) | O(n²) | O(1) | 兩層 for，in-place |
| Merge Sort | O(n log n) | O(n log n) | O(n) | 遞迴分治 + 額外 temp 陣列 |

### 分析 Merge Sort 的時間（最經典的例子）

```cpp
void mergeSort(arr, l, r) {
    if (l >= r) return;         // O(1)
    int m = (l + r) / 2;        // O(1)
    mergeSort(arr, l, m);       // 左半：T(n/2)
    mergeSort(arr, m+1, r);     // 右半：T(n/2)
    merge(arr, l, m, r);        // O(n)
}
```

遞迴公式：T(n) = 2T(n/2) + O(n)

這展開來就是 O(n log n)。直覺理解：
- 每次切一半 → 有 log n 層
- 每層合併需要 O(n)
- → n × log n

---

## 刷題時要注意的面試底線

| 輸入大小 n | 你的演算法至少要 | 不能用 |
|-----------|----------------|--------|
| n ≤ 10 | O(n!) | — |
| n ≤ 20 | O(2ⁿ) | O(n!) |
| n ≤ 100 | O(n⁴) | O(2ⁿ) |
| n ≤ 500 | O(n³) | O(n⁴) |
| n ≤ 2000 | O(n²) | O(n³) |
| n ≤ 10⁵ | O(n log n) | O(n²) |
| n ≤ 10⁶ | O(n) | O(n log n) |
| n ≤ 10⁸ | O(log n) | O(n) |

**面試常見題 n 大約是 10⁴ ~ 10⁵ → 你就要想出 O(n log n) 或更好的解法**

---

## 常犯錯誤

- 把兩個分開的 for 迴圈算成 O(n²) → 實際是 O(n + n) = **O(n)**
- 忘記 STL 操作的複雜度：`unordered_map::find` 是 O(1)，但 `map::find` 是 O(log n)
- 遞迴 depth 太深 → stack overflow（C++ 預設 stack 約 1MB）
- 以為空間複雜度只看 vector，忘記遞迴也算空間

## 相關筆記

- [[Sorting]]
- [[Data Structure]]
