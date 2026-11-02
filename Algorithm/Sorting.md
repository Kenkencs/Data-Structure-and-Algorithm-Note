---
tags: [ds, sorting]
created: 2026-06-17
status: 🟡
---

# Sorting

## 一句話說明
把無序的陣列變成有序（遞增或遞減），是所有算法的基礎。

## 核心操作 & 時間複雜度

| 操作 | 平均 | 最壞 |
|-----|------|------|
| 🫧 Bubble Sort | O(n²) | O(n²) |
| 🔍 Selection Sort | O(n²) | O(n²) |
| 🃏 Insertion Sort | O(n²) | O(n²)（最佳 O(n)）|
| 🧩 Merge Sort | O(n log n) | O(n log n) |

## 跟其他結構的比較

| 排序 | 優點 | 缺點 |
|-----|------|------|
| 🫧 Bubble Sort | 最好寫，有 swapped 優化 | 效率最差，實際幾乎不用 |
| 🔍 Selection Sort | 直覺，交換次數最少 | 不穩定 |
| 🃏 Insertion Sort | 接近有序時 O(n) 超快 | 亂序時跟 bubble 一樣慢 |
| 🧩 Merge Sort | 保證 O(n log n)，穩定 | 需要額外 O(n) 空間 |

## 我會了嗎？🟢 🟡 🔴

- [ ] Bubble Sort：會寫，知道 swapped 優化
- [ ] Selection Sort：會寫，知道跟 bubble 差在哪
- [ ] Insertion Sort：會寫，知道為什麼有序時很快
- [ ] Merge Sort：會寫遞迴版，懂 merge 的邏輯
- [ ] 能用至少一種通過 LeetCode 912

## 易錯點（每次 bug 記這裡）

- Bubble Sort：`j < n - 1 - i`，每輪最後一個已排好不用再比
- Selection Sort：`minIdx` 初始要設 `i`，不是 0
- Insertion Sort：把 `arr[j]` 往右移時要保留 `key`，最後放回 `arr[j + 1]`
- Merge Sort：遞迴終止條件 `l >= r`；mid 用 `l + (r - l) / 2` 防溢出

## 常見題型 & 模板

### Bubble Sort
```cpp
void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        bool swapped = false;
        for (int j = 0; j < n - 1 - i; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
                swapped = true;
            }
        }
        if (!swapped) break;
    }
}
```

### Selection Sort
```cpp
void selectionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        int minIdx = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIdx])
                minIdx = j;
        }
        swap(arr[i], arr[minIdx]);
    }
}
```

### Insertion Sort
```cpp
void insertionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
```

### Merge Sort
```cpp
void merge(vector<int>& arr, int l, int m, int r) {
    vector<int> temp(r - l + 1);
    int i = l, j = m + 1, k = 0;
    while (i <= m && j <= r)
        temp[k++] = arr[i] <= arr[j] ? arr[i++] : arr[j++];
    while (i <= m) temp[k++] = arr[i++];
    while (j <= r) temp[k++] = arr[j++];
    for (int p = 0; p < k; p++)
        arr[l + p] = temp[p];
}

void mergeSort(vector<int>& arr, int l, int r) {
    if (l >= r) return;
    int m = l + (r - l) / 2;
    mergeSort(arr, l, m);
    mergeSort(arr, m + 1, r);
    merge(arr, l, m, r);
}
```

## LeetCode 進度

| 題號  | 題名                  | 難度        | 遍數  | 備註                       |
| --- | ------------------- | --------- | --- | ------------------------ |
| 912 | Sort an Array       | 🟡 Medium |     | 用 merge sort 提交看看        |
| 75  | Sort Colors         | 🟡 Medium |     | 三指針，不用排序函數               |
| 147 | Insertion Sort List | 🟡 Medium |     | linked list 版            |
| 148 | Sort List           | 🟡 Medium |     | linked list 版 merge sort |
| 179 | Largest Number      | 🟡 Medium |     | 自訂排序規則                   |

## 相關筆記

- [[Data Structure]]
