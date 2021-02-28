# Hot 100

## [724. 寻找数组的中心索引](https://leetcode-cn.com/problems/find-pivot-index/)
- stream流的用法有什么好处（实测更慢）

```java

class Solution {
    public int pivotIndex(int[] nums) {
        int total = Arrays.stream(nums).sum();
        int sum = 0;
        for (int i = 0; i < nums.length; ++i) {
            if (2 * sum + nums[i] == total) {
                return i;
            }
            sum += nums[i];
        }
        return -1;
    }
}
```
