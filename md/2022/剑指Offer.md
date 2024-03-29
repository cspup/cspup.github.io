- [剑指 Offer 03. 数组中重复的数字](#剑指-offer-03-数组中重复的数字)
- [剑指 Offer 04. 二维数组中的查找](#剑指-offer-04-二维数组中的查找)
- [剑指 Offer 05. 替换空格](#剑指-offer-05-替换空格)
- [剑指 Offer 06. 从尾到头打印链表](#剑指-offer-06-从尾到头打印链表)
- [剑指 Offer 07. 重建二叉树](#剑指-offer-07-重建二叉树)
- [剑指 Offer 09. 用两个栈实现队列](#剑指-offer-09-用两个栈实现队列)
- [剑指 Offer 10- I. 斐波那契数列](#剑指-offer-10--i-斐波那契数列)
- [剑指 Offer 10- II. 青蛙跳台阶问题](#剑指-offer-10--ii-青蛙跳台阶问题)
- [剑指 Offer 11. 旋转数组的最小数字](#剑指-offer-11-旋转数组的最小数字)
- [剑指 Offer 12. 矩阵中的路径](#剑指-offer-12-矩阵中的路径)
- [剑指 Offer 13. 机器人的运动范围](#剑指-offer-13-机器人的运动范围)
- [剑指 Offer 24. 反转链表](#剑指-offer-24-反转链表)
- [剑指 Offer 30. 包含min函数的栈](#剑指-offer-30-包含min函数的栈)
- [面试题32 - I. 从上到下打印二叉树](#面试题32---i-从上到下打印二叉树)
- [剑指 Offer 32 - II. 从上到下打印二叉树 II](#剑指-offer-32---ii-从上到下打印二叉树-ii)
- [剑指 Offer 32 - III. 从上到下打印二叉树 III](#剑指-offer-32---iii-从上到下打印二叉树-iii)
- [剑指 Offer 35. 复杂链表的复制](#剑指-offer-35-复杂链表的复制)
- [剑指 Offer 53 - I. 在排序数组中查找数字 I](#剑指-offer-53---i-在排序数组中查找数字-i)
- [剑指 Offer 53 - II. 0～n-1中缺失的数字](#剑指-offer-53---ii-0n-1中缺失的数字)
- [面试题50. 第一个只出现一次的字符](#面试题50-第一个只出现一次的字符)
- [剑指 Offer 58 - II. 左旋转字符串](#剑指-offer-58---ii-左旋转字符串)

## 剑指 Offer 03. 数组中重复的数字

找出数组中重复的数字。

在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

示例 1：

输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
 

限制：

2 <= n <= 100000

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

解法一：暴力  

```Java
class Solution {
    public int findRepeatNumber(int[] nums) {
        for (int i=0;i<nums.length-1;i++){
            for (int j=i+1;j<nums.length;j++){
                if (nums[i]==nums[j]){
                    return nums[i];
                }
            }
        }
        return nums[0];
    }
}
```

解法二：使用HashSet  

```Java
class Solution {
    public int findRepeatNumber(int[] nums) {
        HashSet<Integer> set = new HashSet<>();
        for (int i=0;i<nums.length;i++){
            if (!set.add(nums[i])){
                return nums[i];
            }
        }
        return nums[0];
    }
}
```

## 剑指 Offer 04. 二维数组中的查找  

在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

 

示例:

现有矩阵 matrix 如下：

[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
给定 target = 5，返回 true。

给定 target = 20，返回 false。

 

限制：

0 <= n <= 1000

0 <= m <= 1000

链接：https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/

解法一：暴力法直接遍历

解法二：线性查找  

```Java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        if(matrix.length==0||matrix[0].length==0){
            return false;
        }

        int n = 0;
        int m = matrix[0].length-1;

        while (n<matrix.length&&m>=0){
            if (matrix[n][m]==target){
                return true;
            }else if (target>matrix[n][m]){
                n++;
            }else{
                m--;
            }
        }
        
        return false;
    }
}

```

## 剑指 Offer 05. 替换空格
请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

 

示例 1：

输入：s = "We are happy."
输出："We%20are%20happy."
 

限制：

0 <= s 的长度 <= 10000

链接：https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/

```Java
class Solution {
    public String replaceSpace(String s) {
       return s.replaceAll(" ","%20");
    }
}
```


## 剑指 Offer 06. 从尾到头打印链表

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

示例 1：

输入：head = [1,3,2]
输出：[2,3,1]
 

限制：

0 <= 链表长度 <= 10000

链接：https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/

解法一：遍历两遍

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
    public int[] reversePrint(ListNode head) {
        ListNode head1 = head;
        
        int n=0;

        while (head1!=null){
            n++;
            head1 = head1.next;
        }
        

        int[] re = new int[n];

        while (head!=null){
            re[--n] = head.val;
            head = head.next;
        }
        return re;
    }
}
```

解法二：用栈  

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
    public int[] reversePrint(ListNode head) {
        Stack<ListNode> stack = new Stack<ListNode>();
        ListNode temp = head;
        while (temp != null) {
            stack.push(temp);
            temp = temp.next;
        }
        int size = stack.size();
        int[] print = new int[size];
        for (int i = 0; i < size; i++) {
            print[i] = stack.pop().val;
        }
        return print;
    }
}

```

## 剑指 Offer 07. 重建二叉树
输入某二叉树的前序遍历和中序遍历的结果，请构建该二叉树并返回其根节点。

假设输入的前序遍历和中序遍历的结果中都不含重复的数字。


示例 1:

Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
示例 2:

Input: preorder = [-1], inorder = [-1]
Output: [-1]
 

限制：

0 <= 节点个数 <= 5000


解法一：递归构建左右子树  


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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (preorder.length==0||inorder.length==0){
            return null;
        }
        TreeNode head = new TreeNode(preorder[0]);

        if (preorder.length==1||inorder.length==1){
            return head;
        }

        int i = 0;
        
        for (i=0;i<inorder.length;i++){
            if (inorder[i]==preorder[0]){
                break;
            }
        }
        
        int[] leftPreorder = Arrays.copyOfRange(preorder,1,i+1);
        int[] leftInorder = Arrays.copyOfRange(inorder,0,i);
        // 左子树
        head.left = buildTree(leftPreorder,leftInorder);

        if (i>=preorder.length){
            head.right = null;
        }else {
            int[] rightPreorder = Arrays.copyOfRange(preorder,i+1,preorder.length);
            int[] rightInorder = Arrays.copyOfRange(inorder,i+1,inorder.length);

            //右子树
            head.right = buildTree(rightPreorder,rightInorder);
        }


        return head;

    }
}

```

优化：可用HashMap构建节点映射，快速找到节点

```Java
class Solution {
    private Map<Integer, Integer> indexMap;

    public TreeNode myBuildTree(int[] preorder, int[] inorder, int preorder_left, int preorder_right, int inorder_left, int inorder_right) {
        if (preorder_left > preorder_right) {
            return null;
        }

        // 前序遍历中的第一个节点就是根节点
        int preorder_root = preorder_left;
        // 在中序遍历中定位根节点
        int inorder_root = indexMap.get(preorder[preorder_root]);
        
        // 先把根节点建立出来
        TreeNode root = new TreeNode(preorder[preorder_root]);
        // 得到左子树中的节点数目
        int size_left_subtree = inorder_root - inorder_left;
        // 递归地构造左子树，并连接到根节点
        // 先序遍历中「从 左边界+1 开始的 size_left_subtree」个元素就对应了中序遍历中「从 左边界 开始到 根节点定位-1」的元素
        root.left = myBuildTree(preorder, inorder, preorder_left + 1, preorder_left + size_left_subtree, inorder_left, inorder_root - 1);
        // 递归地构造右子树，并连接到根节点
        // 先序遍历中「从 左边界+1+左子树节点数目 开始到 右边界」的元素就对应了中序遍历中「从 根节点定位+1 到 右边界」的元素
        root.right = myBuildTree(preorder, inorder, preorder_left + size_left_subtree + 1, preorder_right, inorder_root + 1, inorder_right);
        return root;
    }

    public TreeNode buildTree(int[] preorder, int[] inorder) {
        int n = preorder.length;
        // 构造哈希映射，帮助我们快速定位根节点
        indexMap = new HashMap<Integer, Integer>();
        for (int i = 0; i < n; i++) {
            indexMap.put(inorder[i], i);
        }
        return myBuildTree(preorder, inorder, 0, n - 1, 0, n - 1);
    }
}

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/solution/mian-shi-ti-07-zhong-jian-er-cha-shu-by-leetcode-s/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```



## 剑指 Offer 09. 用两个栈实现队列
用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

 

示例 1：

输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
示例 2：

输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
提示：

1 <= values <= 10000
最多会对 appendTail、deleteHead 进行 10000 次调用

链接：https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/

方法一：

```Java
class CQueue {

    private Stack<Integer> s1;
     private Stack<Integer> s2;
    public CQueue() {
        s1 = new Stack<>();
        s2 = new Stack<>();
    }
    
    public void appendTail(int value) {
        s1.push(value);
    }
    
    public int deleteHead() {
        if (s1.isEmpty()){
            return -1;
        }

        while (!s1.isEmpty()){
            s2.push(s1.pop());
        }
        int re = s2.pop();

        while(!s2.isEmpty()){
            s1.push(s2.pop());
        }

        return re;
    }
}

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue obj = new CQueue();
 * obj.appendTail(value);
 * int param_2 = obj.deleteHead();
 */

```


## 剑指 Offer 10- I. 斐波那契数列
写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项（即 F(N)）。斐波那契数列的定义如下：

F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

 

示例 1：

输入：n = 2
输出：1
示例 2：

输入：n = 5
输出：5
 

提示：

0 <= n <= 100

链接：https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/

解法一：记忆递归

```Java
class Solution {
    Map<Integer,Integer> map = new HashMap<>();
    public int fib(int n) {
        if (n<2){
            return n;
        }
        if(map.get(n)!=null){
            return map.get(n);
        }
        int sum = (fib(n-1)+fib(n-2))%1000000007;
        map.put(n,sum);
        return sum;
    }
}
```

解法二：动态规划

```Java
class Solution {
    public int fib(int n) {
        final int MOD = 1000000007;
        if (n < 2) {
            return n;
        }
        int p = 0, q = 0, r = 1;
        for (int i = 2; i <= n; ++i) {
            p = q; 
            q = r; 
            r = (p + q) % MOD;
        }
        return r;
    }
}

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/solution/fei-bo-na-qi-shu-lie-by-leetcode-solutio-hbss/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```  


## 剑指 Offer 10- II. 青蛙跳台阶问题
一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

示例 1：

输入：n = 2
输出：2
示例 2：

输入：n = 7
输出：21
示例 3：

输入：n = 0
输出：1
提示：

0 <= n <= 100


可转化为斐波那契数列问题求解。设n阶台阶有f(n)种跳法，最后一步只有两种跳法跳1阶或2阶，则f(n) = f(n-1)+f(n-2)  

解法一：记忆递归

```Java
class Solution {
    HashMap<Integer,Integer> map = new HashMap<>();
    public int numWays(int n) {
        if (n<2){
            return 1;
        }
        if (map.get(n)!=null){
            return map.get(n);
        }else {
            int sum = (numWays(n-1)+numWays(n-2))%1000000007;
            map.put(n,sum);
            return sum;
        }
       
    }
}
```

解法二：动态规划

```Java
class Solution {
    public int numWays(int n) {
        int[] dp = new int[Math.max(n+1,3)];
        dp[0] = 1;
        dp[1] = 1;
        dp[2] = 2;

        for (int i=3;i<=n;i++){
            dp[i] = (dp[i-1]+dp[i-2])%1000000007;
        }
        return dp[n];
    }
}
```


## 剑指 Offer 11. 旋转数组的最小数字
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。

给你一个可能存在 重复 元素值的数组 numbers ，它原来是一个升序排列的数组，并按上述情形进行了一次旋转。请返回旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一次旋转，该数组的最小值为1。  

示例 1：

输入：[3,4,5,1,2]
输出：1
示例 2：

输入：[2,2,2,0,1]
输出：0

链接：https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/

解法一：O(n)的解法

```Java
class Solution {
    public int minArray(int[] numbers) {
        for (int i=0;i<numbers.length;i++){
            if (numbers[0]>numbers[i]){
                return numbers[i];
            }
        }
        return numbers[0];
    }
}
```

解法二：二分查找O(logn)

```Java
class Solution {
    public int minArray(int[] numbers) {
        int low=0;
        int high = numbers.length-1;
        while (low<high){
            // 防止溢出
          int pivot = low +(high-low)/2;

            if (numbers[pivot]>numbers[high]){
                low = pivot+1;
            }
            else if (numbers[pivot]<numbers[high]){
                high = pivot;
            }else{
                high--;
            }
        }

        return numbers[low];
    }
}
```

## 剑指 Offer 12. 矩阵中的路径
给定一个 m x n 二维字符网格 board 和一个字符串单词 word 。如果 word 存在于网格中，返回 true ；否则，返回 false 。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

 

例如，在下面的 3×4 的矩阵中包含单词 "ABCCED"（单词中的字母已标出）。

![图片](http://img.cspup.com/img/f4a753b3dfe643ee8f3c41654222a762.jpeg)

 

示例 1：

输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true
示例 2：

输入：board = [["a","b"],["c","d"]], word = "abcd"
输出：false

链接：https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/

解法一：DFS

```Java
class Solution {
    public boolean exist(char[][] board, String word) {
        char[] words = word.toCharArray();

        for (int i=0;i<board.length;i++){
            for (int j=0;j<board[0].length;j++){
                if(dfs(board,i,j,words,0)){
                    return true;
                }
            }
        }
        return false;
    }

    public boolean dfs (char[][] board,int i,int j,char[] words,int k){
        // 边界
        if (i>=board.length||j>=board[0].length||i<0||j<0||board[i][j] != words[k]){
            return false;
        }
        if(k == words.length - 1) {
            return true;
        }
        
        board[i][j] = '\0';
        // 上下左右搜索
        boolean res = dfs(board,i+1,j,words,k+1)||dfs(board,i-1,j,words,k+1)||dfs(board,i,j+1,words,k+1)||dfs(board,i,j-1,words,k+1);

        board[i][j] = words[k];
        return res;

    }
}
```

## 剑指 Offer 13. 机器人的运动范围
地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

 

示例 1：

输入：m = 2, n = 3, k = 1
输出：3
示例 2：

输入：m = 3, n = 1, k = 0
输出：1
提示：

1 <= n,m <= 100
0 <= k <= 20

链接：https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/

解法一：BFS

```Java
class Solution {
    public int movingCount(int m, int n, int k) {
        if (k==0){
            return 1;
        }

        Queue<int[]> queue = new LinkedList<>();
        int ans = 1;
        int[] dx = {0,1};
        int[] dy = {1,0};

        boolean[][] vis = new boolean[m][n];
        queue.offer(new int[]{0,0});
        vis[0][0] = true;

        while(!queue.isEmpty()){
            int[] cell = queue.poll();
            int x = cell[0];
            int y = cell[1];
            for (int i=0;i<2;i++){
                int tx = x + dx[i];
                int ty = y + dy[i];

                if (tx<0||tx>=m||ty<0||ty>=n||vis[tx][ty]||get(tx)+get(ty)>k){
                    continue;
                }
                queue.offer(new int[]{tx,ty});
                vis[tx][ty] = true;
                ans++;
            }
        }
        return ans;


    }
    int get(int n){
        int res = 0;
        while (n!=0){
            res += n%10;
            n = n/10;
        }
        return res;
    }
}
```



## 剑指 Offer 24. 反转链表
定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

 

示例:

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
 

限制：

0 <= 节点个数 <= 5000

链接：https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/

解法一：使用辅助栈

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
    public ListNode reverseList(ListNode head) {

        if (head==null||head.next==null){
            return head;
        }
        

        Stack<ListNode> stack = new Stack<>();
        while (head!=null){
            stack.push(head);
            head = head.next;
        }
        ListNode head2 = new ListNode(stack.pop().val);
        ListNode head3 = head2;

        while (!stack.isEmpty()){
            head2.next = new ListNode(stack.pop().val);
            head2 = head2.next;

        }

        return head3;
    }
}
```

解法二：迭代

1->2->3->4->null  
pre前一个元素、curr当前元素、next下一个元素
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
    public ListNode reverseList(ListNode head) {
        ListNode pre = null;
        ListNode curr = head;

        while (curr!=null){
            ListNode next = curr.next;
            curr.next = pre;
            pre = curr;
            curr = next;
        }

        return pre;
    }
}
```


## 剑指 Offer 30. 包含min函数的栈
定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

 

示例:

MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
 

提示：

各函数的调用总次数不超过 20000 次

链接：https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/

解法一：使用辅助栈  

```Java
class MinStack {
    private final Stack<Integer> s1;
    private final Stack<Integer> s2;
    /** initialize your data structure here. */
    public MinStack() {
        this.s1 = new Stack<>();
        this.s2 = new Stack<>();
    }

    public void push(int x) {
        s1.push(x);
        if (s2.isEmpty()||x<=s2.peek()){
            s2.push(x);
        }
    }

    public void pop() {
        if (s1.pop().equals(s2.peek())){
            s2.pop();
        }

    }

    public int top() {
        return s1.peek();
    }

    public int min() {
        return s2.peek();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.min();
 */
```



## 面试题32 - I. 从上到下打印二叉树
从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

 

例如:
给定二叉树: [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```
返回：

[3,9,20,15,7]
 

提示：

节点总数 <= 1000


链接：https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/


解法一：层序遍历

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
    public int[] levelOrder(TreeNode root) {
        if (root==null){
            return new int[0];
        }
        List<Integer> list = new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()){
           TreeNode node =  queue.poll();
           list.add(node.val);
           if (node.left!=null){
               queue.offer(node.left);
           }
           if (node.right!=null){
                queue.offer(node.right);
           }
        }

        int[] nums = new int[list.size()];

        // nums = list.stream().mapToInt(Integer::valueOf).toArray();
        for (int i=0;i<list.size();i++>){
            nums[i] = list.get(i);
        }

        return nums;
    }
}
```

## 剑指 Offer 32 - II. 从上到下打印二叉树 II
从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

 

例如:
给定二叉树: [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```
返回其层次遍历结果：

[
  [3],
  [9,20],
  [15,7]
]
 

提示：

节点总数 <= 1000

链接：https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/

解法一：层序遍历，记录每层元素个数  

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
    public List<List<Integer>> levelOrder(TreeNode root) {

        List<List<Integer>> list = new ArrayList<>();
        if (root==null){
            return list;
        }
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        TreeNode end = root;
        while (!queue.isEmpty()){
            List<Integer> list2 = new ArrayList<>();
            // 当前队列的长度,就是这层元素个数
            int len = queue.size();
            // 遍历一层
            for (int i = 0;i < len;i--){
                TreeNode node = queue.poll();
                list2.add(node.val);
                if (node.left!=null){
                    queue.offer(node.left);
                }
                if (node.right!=null){
                    queue.offer(node.right);
                }
            }
            list.add(list2);
        }

        return list;

    }
}
```

## 剑指 Offer 32 - III. 从上到下打印二叉树 III
请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

 

例如:
给定二叉树: [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```
返回其层次遍历结果：

[
  [3],
  [20,9],
  [15,7]
]
 

提示：

节点总数 <= 1000

链接：https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/

解法一：记录层数，反转列表

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> list = new ArrayList<>();
        if (root==null){
            return list;
        }

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        int n = 1;

        while (!queue.isEmpty()){
            List<Integer> list2 = new ArrayList<>();

            int len = queue.size();

            for (int i=0;i<len;i++){
                TreeNode node = queue.poll();
                list2.add(node.val);
                if (node.left!=null){
                    queue.offer(node.left);
                }
                if (node.right!=null){
                    queue.offer(node.right);
                }
            }
// 看题解有大佬用`list.size()%2`判断奇偶
            if (n%2==1){
                list.add(list2);
            }else {
                Collections.reverse(list2);
                list.add(list2);
            }
            n++;
        }


        return list;
    }
}
```




## 剑指 Offer 35. 复杂链表的复制
请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 random 指针指向链表中的任意节点或者 null。

 

示例 1：

![示例 1](http://img.cspup.com/img/b4dffda4006149f084cf8b90916d5748.png)

输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]  

示例 2：

![示例 2](http://img.cspup.com/img/089f394dd7fe4aaeadef231bd5a47c74.png)

输入：head = [[1,1],[2,1]]
输出：[[1,1],[2,1]]  

示例 3：

![示例 3](http://img.cspup.com/img/65a1fc0b59e14e90990082b5fb4a35cc.png)

输入：head = [[3,null],[3,0],[3,null]]
输出：[[3,null],[3,0],[3,null]]  

示例 4：

输入：head = []
输出：[]
解释：给定的链表为空（空指针），因此返回 null。  
 

提示：

-10000 <= Node.val <= 10000
Node.random 为空（null）或指向链表中的节点。
节点数目不超过 1000 。

链接：https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/

解法一：回溯 + 哈希表  

在复制时由于有random的存在，后面的元素可能还未被创建，因此可以让每个节点的拷贝独立。  
用哈希表保存拷贝的元素，对于一个元素now：先进行它本身的拷贝，再分别递归进行now.next的拷贝、now.random的拷贝，就得到了当前节点next和random的元素指针，最后将指针赋给当前元素，就完成了当前元素的完全赋值。

```Java
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/
class Solution {
    Map<Node,Node> cache = new HashMap<>();
    public Node copyRandomList(Node head) {
        if (head==null){
            return null;
        }

        while (!cache.containsKey(head)){
            Node nodeNew = new Node(head.val);
            cache.put(head,nodeNew);
            nodeNew.next = copyRandomList(head.next);
            nodeNew.random = copyRandomList(head.random);
        }

        return cache.get(head);
    }
}
```



## 剑指 Offer 53 - I. 在排序数组中查找数字 I
统计一个数字在排序数组中出现的次数。

 

示例 1:

输入: nums = [5,7,7,8,8,10], target = 8
输出: 2
示例 2:

输入: nums = [5,7,7,8,8,10], target = 6
输出: 0
 

提示：

0 <= nums.length <= 105
-109 <= nums[i] <= 109
nums 是一个非递减数组
-109 <= target <= 109

链接：https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/

解法一：二分查找

从左右两边进行两次查找，找到左边第一个匹配的和右边第一个匹配的，相减就得结果。

```Java

class Solution {
    public int search(int[] nums, int target) {
        
        int left = binarySearch(nums,target,true);
        int right =  binarySearch(nums,target,false)-1;
        if (left<=right&&right<nums.length&&nums[left]==target&&nums[right]==target){
            return right-left+1;
        }
        return 0;
    }

    public int binarySearch(int[] nums,int target,boolean left){
        int low = 0;
        int high = nums.length-1;
        int res = nums.length;

        while(low<=high){
            int mid = low + (high-low)/2;
            if (nums[mid]>target||(left&&nums[mid]>=target)){
                high = mid-1;
                res = mid;
            }else{
                low = mid+1;
            }
        }
        return res;
    }
}
```


## 剑指 Offer 53 - II. 0～n-1中缺失的数字
一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

 

示例 1:

输入: [0,1,3]
输出: 2
示例 2:

输入: [0,1,2,3,4,5,6,7,9]
输出: 8
 

限制：

1 <= 数组长度 <= 10000

链接：https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/

解法一：二分查找

将数组看成左右两块，左侧能和下标对应的，右侧不能对应，找到右侧第一个不能对应下标的就是第一个缺失的数字。
```Java
class Solution {
    public int missingNumber(int[] nums) {
        int low = 0;
        int high = nums.length-1;
        while (low<=high){
            int mid = low+(high-low)/2;
            if (nums[mid]==mid){
                low = mid+1;
            }else{
                high = mid-1;
            }
        }
        return low;
    }
}
```






## 面试题50. 第一个只出现一次的字符
在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

示例 1:

输入：s = "abaccdeff"
输出：'b'
示例 2:

输入：s = "" 
输出：' '
 

限制：

0 <= s 的长度 <= 50000

链接：https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/

解法一：使用哈希表

```Java
class Solution {
    public char firstUniqChar(String s) {
        HashMap<Character,Integer> map = new HashMap<>();

        for (char ch:s.toCharArray()){
            if (map.containsKey(ch)){
                map.put(ch,map.get(ch)+1);
            }else {
                map.put(ch,1);
            }
        }
        for (char ch:s.toCharArray()){
            if (map.get(ch)==1){
                return ch;
            }
        }
        return ' ';
    }
}
```


## 剑指 Offer 58 - II. 左旋转字符串
字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

 

示例 1：

输入: s = "abcdefg", k = 2
输出: "cdefgab"
示例 2：

输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
 

限制：

1 <= k < s.length <= 10000

链接：https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/

解法一：直接使用subString

```Java
class Solution {
    public String reverseLeftWords(String s, int n) {
        return s.substring(n, s.length()) + s.substring(0, n);
    }
}
```

解法二：用StringBuilder

```Java
class Solution {
    public String reverseLeftWords(String s, int n) {
        StringBuilder sb1 = new StringBuilder();
        StringBuilder sb2 = new StringBuilder();

        for (int i=0;i<s.length();i++){
            if (i<n){
                sb2.append(s.charAt(i));
            }else{
                sb1.append(s.charAt(i));
            }
        }
        sb1.append(sb2.toString());

        return sb1.toString();

    }
}

```