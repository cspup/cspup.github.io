- [剑指 Offer 34. 二叉树中和为某一值的路径](#剑指-offer-34-二叉树中和为某一值的路径)
- [剑指 Offer 36. 二叉搜索树与双向链表](#剑指-offer-36-二叉搜索树与双向链表)
- [剑指 Offer 54. 二叉搜索树的第k大节点](#剑指-offer-54-二叉搜索树的第k大节点)
- [剑指 Offer 45. 把数组排成最小的数](#剑指-offer-45-把数组排成最小的数)
- [剑指 Offer 61. 扑克牌中的顺子](#剑指-offer-61-扑克牌中的顺子)
- [剑指 Offer 40. 最小的k个数](#剑指-offer-40-最小的k个数)
- [剑指 Offer 41. 数据流中的中位数](#剑指-offer-41-数据流中的中位数)

## 剑指 Offer 34. 二叉树中和为某一值的路径
给你二叉树的根节点 root 和一个整数目标和 targetSum ，找出所有 从根节点到叶子节点 路径总和等于给定目标和的路径。

叶子节点 是指没有子节点的节点。  

 

示例 1：
![示例1](http://img.cspup.com/img/e3516147a26a4be79f910ba750a0ae96.jpeg)


```
输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：[[5,4,11,2],[5,8,4,5]]
```
示例 2：

![示例2](http://img.cspup.com/img/b242da6a49d44bdc8b58c74b357bc635.jpeg)

```
输入：root = [1,2,3], targetSum = 5
输出：[]
```
示例 3：
```
输入：root = [1,2], targetSum = 0
输出：[]
```
 

提示：

树中节点总数在范围 [0, 5000] 内
-1000 <= Node.val <= 1000
-1000 <= targetSum <= 1000

链接: https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/


解法一：

遍历树

```Java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    List<List<Integer>> ret = new ArrayList<>();
    Deque<Integer> path = new LinkedList<>();
    public List<List<Integer>> pathSum(TreeNode root, int target) {
        dfs(root,target);
        return ret;
    }

    public void dfs(TreeNode root,int target){
        if (root==null){
            return;
        }

        path.offerLast(root.val);
        target -= root.val;
        if (root.left == null && root.right == null && target == 0) {
            ret.add(new LinkedList<Integer>(path));
        }
        dfs(root.left,target);
        dfs(root.right,target);

        // 向上回溯
        path.pollLast();

    }
}
```


## 剑指 Offer 36. 二叉搜索树与双向链表
输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的循环双向链表。要求不能创建任何新的节点，只能调整树中节点指针的指向。

 

为了让您更好地理解问题，以下面的二叉搜索树为例：

 ![1](http://img.cspup.com/img/d8fce592894c4aa0bc39cf6d50371f93.png)



 

我们希望将这个二叉搜索树转化为双向循环链表。链表中的每个节点都有一个前驱和后继指针。对于双向循环链表，第一个节点的前驱是最后一个节点，最后一个节点的后继是第一个节点。

下图展示了上面的二叉搜索树转化成的链表。“head” 表示指向链表中有最小元素的节点。

 
 ![2](http://img.cspup.com/img/fa89c8c25fe04eb3bae5b6fff21dba5b.png)


特别地，我们希望可以就地完成转换操作。当转化完成以后，树中节点的左指针需要指向前驱，树中节点的右指针需要指向后继。还需要返回链表中的第一个节点的指针。


链接：https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/

解法一：中序遍历

二叉搜索树的中序遍历是递增序列,保存前节点，针对当前节点修改它的左指针指向前节点，修改前节点的右指针指向当前节点为后续节点

```Java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val,Node _left,Node _right) {
        val = _val;
        left = _left;
        right = _right;
    }
};
*/
class Solution {
    Node pre,head;
    public Node treeToDoublyList(Node root) {
        if (root==null){
            return null;
        }
        dfs(root);

        head.left = pre;
        pre.right = head;
        return head;
        
    }

    public void dfs(Node root){
        if (root==null){
            return;
        }

        dfs(root.left);

        if (pre!=null){
            // 修改前节点的后续节点
            pre.right = root;
        }else{
            // 没有前节点说明正访问头节点
            head = root;
        }
        // 修改当前访问节点的前节点
        root.left = pre;
        pre = root;

        dfs(root.right);
    }
}

```



## 剑指 Offer 54. 二叉搜索树的第k大节点
给定一棵二叉搜索树，请找出其中第 k 大的节点的值。

 

示例 1:
```
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 4
```
示例 2:
```
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 4
```

限制：

1 ≤ k ≤ 二叉搜索树元素个数

链接：https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/


解法一：

因为是求最大可以使用右中左的中序遍历

```Java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    int ans,k;
    public int kthLargest(TreeNode root, int k) {
        this.k = k;
        dfs(root);
        return ans;
    }

    void dfs(TreeNode root){
        if (root==null){
            return;
        }
        dfs(root.right);
        if (k==0){
           return;
        }
        if (--k==0){
            ans = root.val;
        }

        dfs(root.left);
    }

}
```


## 剑指 Offer 45. 把数组排成最小的数
输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

 

示例 1:
```
输入: [10,2]
输出: "102"
```
示例 2:
```
输入: [3,30,34,5,9]
输出: "3033459"
```

提示:

0 < nums.length <= 100
说明:

输出结果可能非常大，所以你需要返回一个字符串而不是整数
拼接起来的数字可能会有前导 0，最后结果不需要去掉前导 0

链接：https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/


解法一：

修改的冒泡排序，比较ab和ba的字典序，字典序小的在前。  
可使用别的排序方式减少时间复杂度

```Java
class Solution {
    public String minNumber(int[] nums) {
        for (int i=0;i<nums.length-1;i++){
            for (int j=i+1;j<nums.length;j++){
                int tmp = nums[i];
                String a = nums[i]+""+nums[j];
                String b = nums[j]+""+nums[i];
                if (a.compareTo(b)>0){
                    nums[i] = nums[j];
                    nums[j] = tmp;
                }
            }
        }

        StringBuilder sb = new StringBuilder();

        for (int i=0;i<nums.length;i++){
         sb.append(nums[i]);  
        }
        return sb.toString();       
    }
}

```


解法二：修改的快速排序 

```Java
class Solution {
    public String minNumber(int[] nums) {
        String[] strs = new String[nums.length];
        for(int i = 0; i < nums.length; i++)
            strs[i] = String.valueOf(nums[i]);
        quickSort(strs, 0, strs.length - 1);
        StringBuilder res = new StringBuilder();
        for(String s : strs)
            res.append(s);
        return res.toString();
    }
    void quickSort(String[] strs, int l, int r) {
        if(l >= r) return;
        int i = l, j = r;
        String tmp = strs[i];
        while(i < j) {
            while((strs[j] + strs[l]).compareTo(strs[l] + strs[j]) >= 0 && i < j) j--;
            while((strs[i] + strs[l]).compareTo(strs[l] + strs[i]) <= 0 && i < j) i++;
            tmp = strs[i];
            strs[i] = strs[j];
            strs[j] = tmp;
        }
        strs[i] = strs[l];
        strs[l] = tmp;
        quickSort(strs, l, i - 1);
        quickSort(strs, i + 1, r);
    }
}

作者：jyd
链接：https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/solution/mian-shi-ti-45-ba-shu-zu-pai-cheng-zui-xiao-de-s-4/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

```


## 剑指 Offer 61. 扑克牌中的顺子
从若干副扑克牌中随机抽 5 张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。

 

示例 1:
```
输入: [1,2,3,4,5]
输出: True
```

示例 2:
```
输入: [0,0,1,2,5]
输出: True
```

限制：

数组长度为 5 

数组的数取值为 [0, 13] .


链接:https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/

解法一：

排序，计算大小王张数，遍历尝试用大小王补缺，不够补缺或者有对子则不是顺子

```Java
class Solution {
    public boolean isStraight(int[] nums) {
        Arrays.sort(nums);
        int m = 0;
        int pre = nums[0];
        int i=0;
        while (nums[i]==0){
            m++;
            i++;
        }
        for (i=i;i<nums.length-1;i++){
            if (nums[i+1]==nums[i]){
                m=-1;
                break;
            }
            m = m - (nums[i+1]-nums[i]-1);
        }
        return m>=0;
    }
}

```


## 剑指 Offer 40. 最小的k个数
输入整数数组 arr ，找出其中最小的 k 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

 

示例 1：
```
输入：arr = [3,2,1], k = 2
输出：[1,2] 或者 [2,1]
```
示例 2：
```
输入：arr = [0,1,2,1], k = 1
输出：[0]
```

限制：

0 <= k <= arr.length <= 10000
0 <= arr[i] <= 10000

链接:https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/


解法一：排序后取前k个数


```Java
class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        Arrays.sort(arr);
        int[] nums = new int[k];
        for (int i=0;i<k;i++){
            nums[i] = arr[i];
        }
        return nums;
    }
}
```

解法二：冒泡排序只对前k个排序(k为数组长度时可能会超时)

```Java
class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        int[] nums = new int[k];
        for (int i=0;i<k;i++){
            for (int j=i+1;j<arr.length;j++){
                if (arr[i]>arr[j]){
                    int tmp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = tmp;
                }
            }
            nums[i] = arr[i];
        }
        return nums;
    }
}
```

解法三：堆(优先队列)

```Java

class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        int[] vec = new int[k];
        if (k == 0) { // 排除 0 的情况
            return vec;
        }
        PriorityQueue<Integer> queue = new PriorityQueue<Integer>(new Comparator<Integer>() {
            public int compare(Integer num1, Integer num2) {
                return num2 - num1;
            }
        });
        for (int i = 0; i < k; ++i) {
            queue.offer(arr[i]);
        }
        for (int i = k; i < arr.length; ++i) {
            if (queue.peek() > arr[i]) {
                queue.poll();
                queue.offer(arr[i]);
            }
        }
        for (int i = 0; i < k; ++i) {
            vec[i] = queue.poll();
        }
        return vec;
    }
}

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/solution/zui-xiao-de-kge-shu-by-leetcode-solution/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```


解法四：快排思想  
将比第k个小的数放在左边，比第K个小的数放在右边

```Java
class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        randomizedSelected(arr, 0, arr.length - 1, k);
        int[] vec = new int[k];
        for (int i = 0; i < k; ++i) {
            vec[i] = arr[i];
        }
        return vec;
    }

    private void randomizedSelected(int[] arr, int l, int r, int k) {
        if (l >= r) {
            return;
        }
        int pos = randomizedPartition(arr, l, r);
        int num = pos - l + 1;
        if (k == num) {
            return;
        } else if (k < num) {
            randomizedSelected(arr, l, pos - 1, k);
        } else {
            randomizedSelected(arr, pos + 1, r, k - num);
        }
    }

    // 基于随机的划分
    private int randomizedPartition(int[] nums, int l, int r) {
        int i = new Random().nextInt(r - l + 1) + l;
        swap(nums, r, i);
        return partition(nums, l, r);
    }

    private int partition(int[] nums, int l, int r) {
        int pivot = nums[r];
        int i = l - 1;
        for (int j = l; j <= r - 1; ++j) {
            if (nums[j] <= pivot) {
                i = i + 1;
                swap(nums, i, j);
            }
        }
        swap(nums, i + 1, r);
        return i + 1;
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/solution/zui-xiao-de-kge-shu-by-leetcode-solution/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

```


## 剑指 Offer 41. 数据流中的中位数
如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。

例如，

[2,3,4] 的中位数是 3

[2,3] 的中位数是 (2 + 3) / 2 = 2.5

设计一个支持以下两种操作的数据结构：

void addNum(int num) - 从数据流中添加一个整数到数据结构中。
double findMedian() - 返回目前所有元素的中位数。
示例 1：
```
输入：
["MedianFinder","addNum","addNum","findMedian","addNum","findMedian"]
[[],[1],[2],[],[3],[]]
输出：[null,null,null,1.50000,null,2.00000]
```
示例 2：
```
输入：
["MedianFinder","addNum","findMedian","addNum","findMedian"]
[[],[2],[],[3],[]]
输出：[null,null,2.00000,null,2.50000]
 
```
限制：

最多会对 addNum、findMedian 进行 50000 次调用。

链接：https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/


解法一：添加元素时排序（时间复杂度高）

```Java
class MedianFinder {
    List<Integer> list;
    int size;
    /** initialize your data structure here. */
    public MedianFinder() {
        this.list = new ArrayList<>();
        this.size = 0;
    }
    
    public void addNum(int num) {
        list.add(num);
        size++;
        Collections.sort(list);
    }
    
    public double findMedian() {
        if (size%2==0){
            Double d1 = new Double(list.get(size/2));
            Double d2 = new Double(list.get(size/2-1));
            return (d1+d2)/2;
        }else{
            return new Double(list.get(size/2));
        }
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```


解法二：  
使用小顶堆、大顶堆各保留一半元素，中位数可根据两个堆的堆顶元素计算得到

```Java
class MedianFinder {
    Queue<Integer> A, B;
    public MedianFinder() {
        A = new PriorityQueue<>(); // 小顶堆，保存较大的一半
        B = new PriorityQueue<>((x, y) -> (y - x)); // 大顶堆，保存较小的一半
    }
    public void addNum(int num) {
        if(A.size() != B.size()) {
            // 向小顶堆添加元素
            A.add(num);
            // 把小顶堆堆顶元素添加到大顶堆中
            B.add(A.poll());
        } else {
            B.add(num);
            A.add(B.poll());
        }
    }
    public double findMedian() {
        return A.size() != B.size() ? A.peek() : (A.peek() + B.peek()) / 2.0;
    }
}

作者：jyd
链接：https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/solution/mian-shi-ti-41-shu-ju-liu-zhong-de-zhong-wei-shu-y/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```