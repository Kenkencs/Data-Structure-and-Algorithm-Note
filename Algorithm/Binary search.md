[[vector]]  [[Tree]]
## What is it?

二分查找是一种在**有序数组**中查找特定目标值的算法。它通过不断比较中间值（`mid`），将搜索范围缩小一半。

- **逻辑模型**：就像玩“猜数字”游戏，范围是 1-100。你猜 50，告诉你大了，你直接排除 51-100，只在 1-49 里找。
    
- **时间复杂度**：**O(log n)**。相比暴力遍历的 O(n)，这是指数级的提速（在 10 亿数据中，只需要查 30 次）。
    
- **前提条件**：**数组必须有序**（升序或降序）。
    

---

## Why should I use it?（什么时候想到它）

|暴力法 (Linear Search)|**二分查找 (Binary Search)**|
|---|---|
|从前往后一个一个看。|每次直接跳到中间，看方向。|
|**O(n)**，太慢。|**O(log n)**，极快。|
|不要求数组有序。|**必须要求数组有序**。|

> **做题信号：** 只要看到题目说 **“有序数组”**，且让你找某个值、找插入位置、找边界，**脑子里立刻弹窗：二分！**

---
## The Only Template You Need (唯一模板，背熟它)

很多新手纠结于 `while(left < right)` 还是 `while(left <= right)`，导致边界条件总出错。  
**听我的，死磕这一个闭区间模板 `[left, right]`，足以应付 99% 的题目。**

```cpp
#include <vector>
using namespace std;
int binarySearch(vector<int>& nums, int target) {
    int left = 0;
    int right = nums.size() - 1; // 1. 闭区间，左右都能取到
    while (left <= right) {      // 2. 当 left == right 时，区间还有一个元素，依然有效
        // 3. 防溢出写法（而不是 (left+right)/2 ）
        int mid = left + (right - left) / 2; 
        if (nums[mid] == target) {
            return mid;          // 找到了！
        } else if (nums[mid] < target) {
            left = mid + 1;      // 4. target 在右边，排除 mid 和左边
        } else if (nums[mid] > target) {
            right = mid - 1;     // 5. target 在左边，排除 mid 和右边
        }
    }
    return -1; // 没找到
}
```
### 死记这 5 条铁律（保你不溢出、不死循环）：

1. **初始化**：`left = 0`, `right = len - 1`（闭区间包住两端）。
    
2. **循环条件**：`while (left <= right)`（只要还有元素没查，就继续）。
    
3. **计算中点**：`mid = left + (right - left) / 2`（**禁止** `(left+right)/2`，怕溢出）。
    
4. **移动规则**：因为 `mid` 已经查过了，所以**要跨过它**：
    
    - 查左边：`right = mid - 1`
        
    - 查右边：`left = mid + 1`
        
5. **返回值**：找到返回下标；找不到返回 `-1`（或特定的插入点）。
---
## Trap
1. **死循环**：当你写 `while (left < right)` 且更新时写 `left = mid`（没加 1），容易死循环。**解决方案：无脑用 `<=` 模板，并记住 `left = mid + 1` / `right = mid - 1`。**
    
2. **溢出**：`(left + right) / 2` 在 left 和 right 极大时（比如接近 INT_MAX）会整数溢出。**写成 `left + (right - left) / 2` 。** 
    
3. **乱用二分**：看到题目里有无序数组也想用二分。**牢记：只有数组有序（或部分有序），才配叫二分！**

