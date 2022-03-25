- [剑指 Offer 26. 树的子结构](#剑指-offer-26-树的子结构)
- [剑指 Offer 27. 二叉树的镜像](#剑指-offer-27-二叉树的镜像)
- [剑指 Offer 28. 对称的二叉树](#剑指-offer-28-对称的二叉树)
- [剑指 Offer 63. 股票的最大利润](#剑指-offer-63-股票的最大利润)
- [剑指 Offer 42. 连续子数组的最大和](#剑指-offer-42-连续子数组的最大和)
- [剑指 Offer 47. 礼物的最大价值](#剑指-offer-47-礼物的最大价值)
- [剑指 Offer 46. 把数字翻译成字符串](#剑指-offer-46-把数字翻译成字符串)
- [剑指 Offer 48. 最长不含重复字符的子字符串](#剑指-offer-48-最长不含重复字符的子字符串)
- [剑指 Offer 18. 删除链表的节点](#剑指-offer-18-删除链表的节点)
- [剑指 Offer 22. 链表中倒数第k个节点](#剑指-offer-22-链表中倒数第k个节点)
- [剑指 Offer 25. 合并两个排序的链表](#剑指-offer-25-合并两个排序的链表)
- [剑指 Offer 52. 两个链表的第一个公共节点](#剑指-offer-52-两个链表的第一个公共节点)
- [剑指 Offer 21. 调整数组顺序使奇数位于偶数前面](#剑指-offer-21-调整数组顺序使奇数位于偶数前面)
- [剑指 Offer 57. 和为s的两个数字](#剑指-offer-57-和为s的两个数字)
- [剑指 Offer 58 - I. 翻转单词顺序](#剑指-offer-58---i-翻转单词顺序)

## 剑指 Offer 26. 树的子结构
输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)

B是A的子结构， 即 A中有出现和B相同的结构和节点值。

例如:
给定的树 A:
```
     3
    / \
   4   5
  / \
 1   2
```
给定的树 B：
```
   4 
  /
 1
```
返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。

示例 1：

输入：A = [1,2,3], B = [3,1]
输出：false
示例 2：

输入：A = [3,4,5,1,2], B = [4,1]
输出：true
限制：

0 <= 节点个数 <= 10000

链接：https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/  


解法一：递归  


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
    public boolean isSubStructure(TreeNode A, TreeNode B) {
        if (B==null||A==null){
            return false;
        }
        // 判断这棵树或左右子树
        return contains(A,B)||isSubStructure(A.left,B)||isSubStructure(A.right,B);

    }

    public boolean contains(TreeNode A,TreeNode B){
        if (B==null){
            return true;
        }
        if (A==null||A.val!=B.val){
            return false;
        }
        // 递归判断左右子树
        return contains(A.left,B.left)&&contains(A.right,B.right);
    }
}

```


## 剑指 Offer 27. 二叉树的镜像
请完成一个函数，输入一个二叉树，该函数输出它的镜像。

例如输入：
```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
镜像输出：

     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

 

示例 1：

输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]
 

限制：

0 <= 节点个数 <= 1000

链接：https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/

解法一：递归

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
    public TreeNode mirrorTree(TreeNode root) {
        if (root==null){
            return null;
        }
        TreeNode newTree =  new TreeNode(root.val);
        newTree.left = mirrorTree(root.right);
        newTree.right = mirrorTree(root.left);
        
        return newTree;
        
    }
}

```


## 剑指 Offer 28. 对称的二叉树
请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

    1
   / \
  2   2
 / \ / \
3  4 4  3
但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

    1
   / \
  2   2
   \   \
   3    3

 

示例 1：

输入：root = [1,2,2,3,4,4,3]
输出：true
示例 2：

输入：root = [1,2,2,null,3,null,3]
输出：false
 

限制：

0 <= 节点个数 <= 1000

链接：https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/

解法一：递归

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
    public boolean isSymmetric(TreeNode root) {
        if (root==null){
            return true;
        }
        // 递归
        return recur(root.left,root.right);

    }

    public boolean recur(TreeNode A,TreeNode B){
        if (A==null&&B==null){
            return true;
        }
        // 失败条件
        if (A==null||B==null||A.val!=B.val){
            return false;
        }
        // 比较A的左子树和B的右子树，A的右子树和B的左子树
        return recur(A.left,B.right)&&recur(A.right,B.left);
    }
}
```


## 剑指 Offer 63. 股票的最大利润
假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？

 

示例 1:

输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
示例 2:

输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
 

限制：

0 <= 数组长度 <= 10^5

链接：https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/  

解法一：暴力

```Java
class Solution {
    public int maxProfit(int[] prices) {
        int maxProfit = 0;
        for (int i=0;i<prices.length;i++){
            for (int j=i;j<prices.length;j++){
                if (prices[j]-prices[i]>maxProfit){
                    maxProfit = prices[j]-prices[i];
                }
            }
        }

        return maxProfit;
    }
}

```

解法二：一次遍历，记录当前点之前的最小值，计算最大利润

最大利润 = Max(之前的最大利润，现价 - 之前的最小花费)
```Java
public class Solution {
    public int maxProfit(int prices[]) {
        int minprice = Integer.MAX_VALUE;
        int maxprofit = 0;
        for (int i = 0; i < prices.length; i++) {
            if (prices[i] < minprice) {
                minprice = prices[i];
            } else if (prices[i] - minprice > maxprofit) {
                maxprofit = prices[i] - minprice;
            }
        }
        return maxprofit;
    }
}

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/solution/gu-piao-de-zui-da-li-run-by-leetcode-sol-0l1g/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```


## 剑指 Offer 42. 连续子数组的最大和
输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。

 

示例1:

输入: nums = [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
 

提示：

1 <= arr.length <= 10^5
-100 <= arr[i] <= 100
注意：本题与主站 53 题相同：https://leetcode-cn.com/problems/maximum-subarray/

链接：https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/

解法一：动态规划

求出每个位置的最大值，返回最大值中最大的数。  
对于一个位置的最大值，dp[i] = Max(dp[i-1]+nums[i]，nums[i])

```Java
class Solution {
    public int maxSubArray(int[] nums) {
        int max = nums[0];
        int[] dp = new int[nums.length];
        dp[0] = nums[0];
        for (int i=1;i<nums.length;i++){
            if (nums[i]+dp[i-1]>=nums[i]){
                dp[i] = nums[i]+dp[i-1];
            }else{
                dp[i] = nums[i];
            }
            if (max<dp[i]){
                max = dp[i];
            }
        }

        return max;
    }
}
```

## 剑指 Offer 47. 礼物的最大价值
在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

 

示例 1:

输入: 
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 12
解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物
 

提示：

0 < grid.length <= 200
0 < grid[0].length <= 200

链接：https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/

解法一：动态规划

用一个数组保存当前位置所能得到的最大价值，最后数组右下角就是整个棋盘能得到的最大价值。  

由于仅能向右或向下移动，(i,j)的最大价值为Max（左边值，上边值）+ (i,j)的值，公式为：dp[i][j] = Max(dp[i-1][j],dp[i][j-1]) + grid[i][j]

```Java
class Solution {
    public int maxValue(int[][] grid) {

        int[][] dp = new int[grid.length][grid[0].length];
        dp[0][0] = grid[0][0];
        int m = grid.length;
        int n = grid[0].length;

        // 先初始化第一行和第一列，减少后面再处理
        for (int i=1;i<grid.length;i++){
            dp[i][0] = dp[i-1][0]+grid[i][0];
        }
        for (int i=1;i<grid[0].length;i++){
            dp[0][i] = dp[0][i-1]+grid[0][i];
        }

        for (int i=1;i<grid.length;i++){
            for (int j=1;j<grid[0].length;j++){
                dp[i][j] = Math.max(dp[i-1][j],dp[i][j-1])+grid[i][j];
            }
        }

        return dp[m-1][n-1];
    }
}
```

## 剑指 Offer 46. 把数字翻译成字符串
给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

 

示例 1:

输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
 

提示：

0 <= num < 231

链接：https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/

解法一：动态规划

将求解过程分解，12258分解为：1->12->122->1225->12258。  
每个数字有两种情况：可以和前面数字组合为一个字母（和前面的数字组成大于9小于26的数字）对结果贡献的递推方程：f(i) = f(i-1) + f(i-2)；不可以和前面数字组合为一个字母，对结果贡献为0。针对不同情况进行判断.

```Java
class Solution {
    public int translateNum(int num) {
        String str = String.valueOf(num);

        int[] dp = new int[str.length()];
        dp[0] = 1;

        for (int i=1;i<str.length();i++){
             int i1 = Integer.parseInt(str.substring(i - 1, i + 1));
            if (i1<26&& i1 >9){
                if (i>1){
                    dp[i] = dp[i-1] + dp[i-2];
                }else{
                    dp[i] = dp[i-1]+1;
                }

            }else{
                dp[i] = dp[i-1];
            }

        }
        return dp[str.length()-1];

    }
}
```


## 剑指 Offer 48. 最长不含重复字符的子字符串
请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

 

示例 1:

输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
示例 2:

输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
示例 3:

输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
 

提示：

s.length <= 40000

链接：https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/

解法一：遍历生成子串

按条件生成所有不重复子串，用一个变量保存最长的子串


```Java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s==null||s.isEmpty()){
            return 0;
        }
        String maxS = String.valueOf(s.charAt(0));
        StringBuilder stringBuilder = new StringBuilder();
        stringBuilder.append(s.charAt(0));


        for (int i=1;i<s.length();i++){

            if (stringBuilder.indexOf(String.valueOf(s.charAt(i)))>-1){
                if (maxS.length()<stringBuilder.length()){
                    maxS = stringBuilder.toString();
                }
                stringBuilder = new StringBuilder(stringBuilder.substring(stringBuilder.indexOf(String.valueOf(s.charAt(i)))+1, stringBuilder.length()));
            }
            stringBuilder.append(s.charAt(i));
            if (maxS.length()<stringBuilder.length()){
                maxS = stringBuilder.toString();
            }
        }
        
        return maxS.length();
    }
}
```

解法二：动态规划 + 哈希表


双指针，i记录元素首次出现位置，j记录本次出现位置，相减就可得不含重复字符的长度。需要用一个哈希表记录元素的位置

```Java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> dic = new HashMap<>();
        int res = 0, tmp = 0;
        for(int j = 0; j < s.length(); j++) {
            int i = dic.getOrDefault(s.charAt(j), -1); // 获取索引 i
            dic.put(s.charAt(j), j); // 更新哈希表
            tmp = tmp < j - i ? tmp + 1 : j - i; // dp[j - 1] -> dp[j]
            res = Math.max(res, tmp); // max(dp[j - 1], dp[j])
        }
        return res;
    }
}

作者：jyd
链接：https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/solution/mian-shi-ti-48-zui-chang-bu-han-zhong-fu-zi-fu-d-9/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

## 剑指 Offer 18. 删除链表的节点
给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

返回删除后的链表的头节点。

注意：此题对比原题有改动

示例 1:

输入: head = [4,5,1,9], val = 5
输出: [4,1,9]
解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
示例 2:

输入: head = [4,5,1,9], val = 1
输出: [4,5,9]
解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.
 

说明：

题目保证链表中节点的值互不相同
若使用 C 或 C++ 语言，你不需要 free 或 delete 被删除的节点

链接：https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof/

解法一：

```Java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode deleteNode(ListNode head, int val) {
        if (head==null){
            return null;
        }
        if (head.val == val){
            return head.next;
        }
        ListNode h1 = head;
        
        ListNode last = head;
        head = head.next;
        while (head!=null){
            if (head.val==val){
                last.next = head.next;
                break;
            }else{
                last = head;
                head = head.next;
            }
        }
        return h1;
    }
}
```

## 剑指 Offer 22. 链表中倒数第k个节点
输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。

例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。

 

示例：

给定一个链表: 1->2->3->4->5, 和 k = 2.

返回链表 4->5.

链接：https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/


解法一：双指针(快慢指针)


```Java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode getKthFromEnd(ListNode head, int k) {
        ListNode p1 = head;
        ListNode p2 = head;
        int i=0;
        while (p2!=null&&i++<k){
            p2 = p2.next;
        }

        while (p2!=null){
            p1 = p1.next;
            p2 = p2.next;
        }

        return p1;
    }
}
```


## 剑指 Offer 25. 合并两个排序的链表
输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

示例1：

输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
限制：

0 <= 链表长度 <= 1000


解法一：遍历、比较、逐个添加到新的头节点

```Java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1==null){
            return l2;
        }
        if (l2==null){
            return l1;
        }
        ListNode head;
        ListNode l;
        if (l1.val>l2.val){
            l = l2;
            l2 = l2.next;
        }else{
            l = l1;
            l1 = l1.next;
        }
        head = l;
        while (l1!=null&&l2!=null){
            if (l1.val<l2.val){
                l.next = l1;
                l = l.next;
                l1 = l1.next;
            }else {
                l.next = l2;
                l = l.next;
                l2 = l2.next;
            }
        }
        while (l1!=null){
            l.next = l1;
            l = l.next;
            l1 = l1.next;
        }
        while (l2!=null){
            l.next = l2;
            l = l.next;
            l2 = l2.next;
        }
        return head;
    }
}
```


## 剑指 Offer 52. 两个链表的第一个公共节点
输入两个链表，找出它们的第一个公共节点。

如下面的两个链表：
![示例0](http://img.cspup.com/img/79da65cc25c140d485edd51a40696d7d.png)



在节点 c1 开始相交。

 

示例 1：
![示例1](http://img.cspup.com/img/4aed31d1cd64468bbfe014ee9545df9e.png)

输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Reference of the node with value = 8
输入解释：相交节点的值为 8 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
 

示例 2：

![示例2](http://img.cspup.com/img/0e130aa40d3246b38f54097998b4fc4e.png)




输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Reference of the node with value = 2
输入解释：相交节点的值为 2 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。
 

示例 3：

![示例3](http://img.cspup.com/img/ac6f5e905dc54587af1012efba9471cd.png)




输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
输出：null
输入解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
解释：这两个链表不相交，因此返回 null。
 

注意：

如果两个链表没有交点，返回 null.
在返回结果后，两个链表仍须保持原有的结构。
可假定整个链表结构中没有循环。
程序尽量满足 O(n) 时间复杂度，且仅用 O(1) 内存。
本题与主站 160 题相同：https://leetcode-cn.com/problems/intersection-of-two-linked-lists/

链接：https://leetcode-cn.com/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/


解法一：计算两个链表的长度差，让长的链表先走几步，再让两个链表同步遍历寻找相同的节点

```Java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        int a=0;
        int b=0;
        ListNode h1 = headA;
        ListNode h2 = headB;
        while (headA!=null&&headB!=null){
            headA = headA.next;
            headB = headB.next;
            a++;
            b++;
        }
        while (headA!=null){
            a++;
            headA = headA.next;
        }
        while (headB!=null){
            b++;
            headB = headB.next;
        }

        if (a>b){
            for (int i=0;i<a-b;i++){
                h1 = h1.next;
            }
        }
        if (b>a){
            for (int i=0;i<b-a;i++){
                h2 = h2.next;
            }
        }

        while(h1!=null&&h2!=null){
            if (h1==h2){
                return h1;
            }else{
                h1 = h1.next;
                h2 = h2.next;
            }
        }
        return null;
    }
}
```


解法二：双指针

```Java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) {
            return null;
        }
        ListNode pA = headA, pB = headB;
        while (pA != pB) {
            pA = pA == null ? headB : pA.next;
            pB = pB == null ? headA : pB.next;
        }
        return pA;
    }
}

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/solution/liang-ge-lian-biao-de-di-yi-ge-gong-gong-pzbs/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```


## 剑指 Offer 21. 调整数组顺序使奇数位于偶数前面
输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数在数组的前半部分，所有偶数在数组的后半部分。

 

示例：

输入：nums = [1,2,3,4]
输出：[1,3,2,4] 
注：[3,1,2,4] 也是正确的答案之一。
 

提示：

1. 0 <= nums.length <= 50000
2. 0 <= nums[i] <= 10000

链接：https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/


解法一：双指针

```Java
class Solution {
    public int[] exchange(int[] nums) {
        int low = 0;
        int high = nums.length-1;

        while (low<high){
            if (nums[low]%2==0&&nums[high]%2!=0){
                int tmp = nums[low];
                nums[low] = nums[high];
                nums[high] = tmp;
                low++;
                high--;
            }else if (nums[low]%2!=0&&nums[high]%2==0){
                low++;
                high--;
            }else if (nums[low]%2==0&&nums[high]%2==0){
                high--;
            }else if (nums[low]%2!=0&&nums[high]%2!=0){
                low++;
            }
        }
        return nums;

    }
}
```


## 剑指 Offer 57. 和为s的两个数字
输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。

 

示例 1：

输入：nums = [2,7,11,15], target = 9
输出：[2,7] 或者 [7,2]
示例 2：

输入：nums = [10,26,30,31,47,60], target = 40
输出：[10,30] 或者 [30,10]
 

限制：

1. 1 <= nums.length <= 10^5
2. 1 <= nums[i] <= 10^6

链接：https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/

解法一：双指针


```Java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int low = 0;
        int high = nums.length-1;

        while (low<high){
            if (nums[low]+nums[high]<target){
                low++;
            }else if (nums[low]+nums[high]>target){
                high--;
            }else{
                int[] n = new int[2];
                n[0] = nums[low];
                n[1] = nums[high];
                return n;
            }
        }
        return null;
    }
}
```


## 剑指 Offer 58 - I. 翻转单词顺序
输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"。

 

示例 1：

输入: "the sky is blue"
输出: "blue is sky the"
示例 2：

输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
示例 3：

输入: "a good   example"
输出: "example good a"
解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
 

说明：

无空格字符构成一个单词。
输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。

链接：https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/


解法一：使用Java库函数和正则

```Java
class Solution {
    public String reverseWords(String s) {
        String[] strs = s.split("\\s+");
        int low = 0;
        int high = strs.length-1;
        while (low<high){
            String tmp = strs[low];
            strs[low] = strs[high];
            strs[high] = tmp;
            low++;
            high--;
        }

        return  String.join(" ", strs).trim();
    }
}
```

解法二：双指针


```Java
class Solution {
    public String reverseWords(String s) {
        s = s.trim(); // 删除首尾空格
        int j = s.length() - 1, i = j;
        StringBuilder res = new StringBuilder();
        while(i >= 0) {
            while(i >= 0 && s.charAt(i) != ' ') i--; // 搜索首个空格
            res.append(s.substring(i + 1, j + 1) + " "); // 添加单词
            while(i >= 0 && s.charAt(i) == ' ') i--; // 跳过单词间空格
            j = i; // j 指向下个单词的尾字符
        }
        return res.toString().trim(); // 转化为字符串并返回
    }
}

作者：jyd
链接：https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/solution/mian-shi-ti-58-i-fan-zhuan-dan-ci-shun-xu-shuang-z/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```