# 和为 K 的子数组

给你一个整数数组 `nums` 和一个整数 `k` ，请你统计并返回 *该数组中和为 `k` 的子数组的个数* 。

子数组是数组中元素的连续非空序列。

 

**示例 1：**

```
输入：nums = [1,1,1], k = 2
输出：2
```

**示例 2：**

```
输入：nums = [1,2,3], k = 3
输出：2
```

 

**提示：**

- `1 <= nums.length <= 2 * 104`
- `-1000 <= nums[i] <= 1000`
- `-107 <= k <= 107`



---


```csharp
// 前缀和 + 字典
// k 的本质: [j+1 ... i] 的和
// k = sum[i] - sum[j]
// sum[j] = sum[i] - k
// 遍历数组，检查当前 sum_j 是否存在字典中，如果存在，计数器cnt + 存在的次数
// 如果字典不存在当前 sum_i，在字典中添加，并将次数设为 1

public class Solution {
    public int SubarraySum(int[] nums, int k) {
        Dictionary<int, int> dic = new Dictionary<int, int>();
        /*
        相当于提前执行以下操作：
        sum 初始值为 0
        if (!dic.ContainsKey(sum)) {
                dic[sum] = 0;
            }

            dic[sum]++;
        */
        dic[0] = 1;

        int sum = 0, cnt = 0;

        foreach (int num in nums) {
            sum += num;

            if (dic.ContainsKey(sum - k)) {
                cnt += dic[sum - k];
            }

            if (!dic.ContainsKey(sum)) {
                dic[sum] = 0;
            }

            dic[sum]++;
        }

        return cnt;
    }
}
```

