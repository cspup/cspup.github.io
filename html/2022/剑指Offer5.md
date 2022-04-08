- [剑指 Offer 59 - I. 滑动窗口的最大值](#剑指-offer-59---i-滑动窗口的最大值)
- [剑指 Offer 59 - II. 队列的最大值](#剑指-offer-59---ii-队列的最大值)

## 剑指 Offer 59 - I. 滑动窗口的最大值  

给定一个数组 nums 和滑动窗口的大小 k，请找出所有滑动窗口里的最大值。

**示例:**
```
输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
输出: [3,3,5,5,6,7] 
解释: 

  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```
 提示：

你可以假设 k 总是有效的，在输入数组不为空的情况下，1 ≤ k ≤ 输入数组的大小。

链接：https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/

解法一：优先队列（堆）

```Java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int n = nums.length;
        PriorityQueue<int[]> pq = new PriorityQueue<int[]>(new Comparator<int[]>() {
            public int compare(int[] pair1, int[] pair2) {
                return pair1[0] != pair2[0] ? pair2[0] - pair1[0] : pair2[1] - pair1[1];
            }
        });
        for (int i = 0; i < k; ++i) {
            pq.offer(new int[]{nums[i], i});
        }
        int[] ans = new int[n - k + 1];
        ans[0] = pq.peek()[0];
        for (int i = k; i < n; ++i) {
            pq.offer(new int[]{nums[i], i});
            while (pq.peek()[1] <= i - k) {
                pq.poll();
            }
            ans[i - k + 1] = pq.peek()[0];
        }
        return ans;
    }
}

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/solution/hua-dong-chuang-kou-de-zui-da-zhi-by-lee-ymyo/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

解法二：单调队列(单调递减的队列)

```Java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int n = nums.length;
        Deque<Integer> deque = new LinkedList<Integer>();
        for (int i = 0; i < k; ++i) {
            while (!deque.isEmpty() && nums[i] >= nums[deque.peekLast()]) {
                deque.pollLast();
            }
            deque.offerLast(i);
        }

        int[] ans = new int[n - k + 1];
        ans[0] = nums[deque.peekFirst()];
        for (int i = k; i < n; ++i) {
            while (!deque.isEmpty() && nums[i] >= nums[deque.peekLast()]) {
                deque.pollLast();
            }
            deque.offerLast(i);
            while (deque.peekFirst() <= i - k) {
                deque.pollFirst();
            }
            ans[i - k + 1] = nums[deque.peekFirst()];
        }
        return ans;
    }
}

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/solution/hua-dong-chuang-kou-de-zui-da-zhi-by-lee-ymyo/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```


## 剑指 Offer 59 - II. 队列的最大值
请定义一个队列并实现函数 max_value 得到队列里的最大值，要求函数max_value、push_back 和 pop_front 的均摊时间复杂度都是O(1)。

若队列为空，pop_front 和 max_value 需要返回 -1

示例 1：
```
输入: 
["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
[[],[1],[2],[],[],[]]
输出: [null,null,null,2,1,2]
```
示例 2：
```
输入: 
["MaxQueue","pop_front","max_value"]
[[],[],[]]
输出: [null,-1,-1]
``` 

限制：

1 <= push_back,pop_front,max_value的总操作数 <= 10000
1 <= value <= 10^5

链接：https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/

解法一：维护一个普通队列和单调队列

```Java
class MaxQueue {
    Queue<Integer> queue;
    Deque<Integer> deque;
    public MaxQueue() {
        this.queue = new LinkedList<>();
        this.deque = new LinkedList<Integer>();
    }
    
    public int max_value() {
        if (deque.isEmpty()){
            return -1;
        }
        return deque.peekFirst();
    }
    
    public void push_back(int value) {
        queue.offer(value);
        while (!deque.isEmpty()&&deque.peekLast()<value){
            deque.pollLast();
        }
        deque.offerLast(value);
    }
    
    public int pop_front() {
        if (queue.isEmpty()) {
            return -1;
        }
        int ans = queue.poll();
        if (ans == deque.peekFirst()) {
            deque.pollFirst();
        }
        return ans;
    }
}

/**
 * Your MaxQueue object will be instantiated and called as such:
 * MaxQueue obj = new MaxQueue();
 * int param_1 = obj.max_value();
 * obj.push_back(value);
 * int param_3 = obj.pop_front();
 */
```