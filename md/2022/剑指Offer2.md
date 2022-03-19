- [剑指 Offer 26. 树的子结构](#剑指-offer-26-树的子结构)
- [剑指 Offer 27. 二叉树的镜像](#剑指-offer-27-二叉树的镜像)
- [剑指 Offer 28. 对称的二叉树](#剑指-offer-28-对称的二叉树)

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