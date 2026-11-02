# Stack

[[vector]]

## What is it？

- A container adopter 
- Last in first out (LIFO)
	- eg: using google -> go to youtube -> go to X -> return to x -> return to youtube -> return to google

- `push`、`pop`、`top` **O(1)**

---
## Why should i use?

**Stack** is a way to avoid huge time complexity 
Sometime brute force can't solve the case

**无序 + 嵌套结构 + 回溯场景 + 需要撤销** → 用 `stack`。  
**其余情况（需要随机访问、需要遍历中间元素）** → 优先考虑 `vector` 或 `deque`。


---
## How to use

```cpp
#include <stack>
```
include the header


```cpp
stack <int> mystack 
```
initialize

| 操作          | 函数名                | 作用说明                                 |
| ----------- | ------------------ | ------------------------------------ |
| **入栈（增）**   | `push(value)`      | 将元素拷贝/移动进栈顶                          |
| **原地构造入栈**  | `emplace(args...)` | C++11 起，直接在栈内构造元素，避免拷贝（比 `push` 更高效） |
| **出栈（删）**   | `pop()`            | **删除**栈顶元素（**注意：没有返回值！**）            |
| **查看栈顶（查）** | `top()`            | 返回栈顶元素的**引用**（可读可修改）                 |
| **判空**      | `empty()`          | 栈为空返回 `true`，否则 `false`              |
| **大小**      | `size()`           | 返回栈中元素的个数（`size_t` 类型）               |
```cpp
while (!s.empty()) {            // 当栈不为空
        int current = s.top();      // 先获取栈顶
        s.pop();                    // 再弹出
    }
```
To get out of the stack, we should first check the stack

---
## Stack overflow

Memory is boom and there are no more place to use



----

# Queue

## What is Queue

 A container adopter 
- First in first out (FIFO)
	- eg: angry bird 

- `push`（入队）、`pop`（出队）、`front`（队首）、`back`（队尾）操作均为 **O(1)** 

---
## Why should i use it

遇到“排队”、“缓冲”、“先到先得”的场景，用 `queue` 准没错。

1. **广度优先搜索（BFS）**：走迷宫找最短路径、社交网络找好友关系（一度二度好友），一层一层往外扩，**先查到的那层必须先处理**，这是队列的经典主场。
    
2. **任务调度（生产者-消费者）**：打印机任务队列、消息队列（MQ）。你把任务扔进队尾，处理程序从队首取任务，谁先来谁先被处理。
    
3. **请求缓冲**：高并发下服务器把请求排队，防止瞬间流量冲垮系统。
    

**注意**：如果数据需要“后来先处理”（如递归回溯），请用 `stack`；如果数据需要“先来先处理”（如按顺序派发），请用 `queue`。


---
## Method

| 操作           | 函数名                | 作用说明                                 |
| ------------ | ------------------ | ------------------------------------ |
| **入队列（增）**   | `push(value)`      | 将元素拷贝/移动进栈顶                          |
| **原地构造入队列**  | `emplace(args...)` | C++11 起，直接在栈内构造元素，避免拷贝（比 `push` 更高效） |
| **出队列（删）**   | `pop()`            | **删除**栈顶元素（**注意：没有返回值！**）            |
| **查看队列顶（查）** | `front()`          | 返回栈顶元素的**引用**（可读可修改）                 |
| **判空**       | `empty()`          | 栈为空返回 `true`，否则 `false`              |
| **大小**       | `size()`           | 返回栈中元素的个数（`size_t` 类型）               |
| **查最后**      | `back()`           | 查看最后一个元素                             |

大部分和stack 一样，只不过有个back
