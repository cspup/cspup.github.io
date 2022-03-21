- [剑指 Offer 26. 树的子结构](#剑指-offer-26-树的子结构)
- [剑指 Offer 27. 二叉树的镜像](#剑指-offer-27-二叉树的镜像)
- [剑指 Offer 28. 对称的二叉树](#剑指-offer-28-对称的二叉树)
- [剑指 Offer 63. 股票的最大利润](#剑指-offer-63-股票的最大利润)
- [剑指 Offer 42. 连续子数组的最大和](#剑指-offer-42-连续子数组的最大和)
- [剑指 Offer 47. 礼物的最大价值](#剑指-offer-47-礼物的最大价值)

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

