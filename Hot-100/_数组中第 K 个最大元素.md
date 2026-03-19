给定整数数组 `nums` 和整数 `k`，请返回数组中第 `k` 个最大的元素。

请注意，你需要找的是数组排序后的第 `k` 个最大的元素，而不是第 `k` 个不同的元素。

你必须设计并实现时间复杂度为 `O(n)` 的算法解决此问题。

 

**示例 1:**

```
输入: [3,2,1,5,6,4], k = 2
输出: 5
```

**示例 2:**

```
输入: [3,2,3,1,2,4,5,5,6], k = 4
输出: 4
```

 

**提示：**

- `1 <= k <= nums.length <= 105`
- `-104 <= nums[i] <= 104`



---

## 优先队列写法

```csharp
// 优先队列 PriorityQueue (默认为最小堆)
// 将数输入优先队列，优先级为数的本身
// 出队，直到剩余 K 个数
// 返回堆顶

public class Solution {
    public int FindKthLargest(int[] nums, int k) {
        PriorityQueue<int, int> minHeap = new PriorityQueue<int, int>();

        foreach (int num in nums) {
            // 优先级为数的本身
            minHeap.Enqueue(num, num);
        }
		
        // 最后剩下 k 个数
        // 栈顶为第 K 个最大数
        while (minHeap.Count > k) {
            minHeap.Dequeue();
        }

        return minHeap.Peek();
    }
}
```

| 方法                                                       | 说明                                 | 示例                                               |
| ---------------------------------------------------------- | ------------------------------------ | -------------------------------------------------- |
| `Enqueue(TElement element, TPriority priority)`            | 入队：添加元素及其优先级             | `pq.Enqueue("紧急任务", 1);`                       |
| `Dequeue()`                                                | 出队：移除并返回当前优先级最高的元素 | `string task = pq.Dequeue();`                      |
| `Peek()`                                                   | 查看但不移除堆顶元素（最高优先级）   | `string top = pq.Peek();`                          |
| `Count`                                                    | 获取队列中元素数量                   | `int n = pq.Count;`                                |
| `Clear()`                                                  | 清空队列                             | `pq.Clear();`                                      |
| `TryDequeue(out TElement element, out TPriority priority)` | 安全出队（避免空队异常）             | `if (pq.TryDequeue(out var e, out var p)) { ... }` |

---

## 随机选择写法

