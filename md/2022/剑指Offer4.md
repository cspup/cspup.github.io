- [剑指 Offer 15. 二进制中1的个数](#剑指-offer-15-二进制中1的个数)
- [剑指 Offer 65. 不用加减乘除做加法](#剑指-offer-65-不用加减乘除做加法)

## 剑指 Offer 15. 二进制中1的个数
编写一个函数，输入是一个无符号整数（以二进制串的形式），返回其二进制表达式中数字位数为 '1' 的个数（也被称为 汉明重量).）。

 

提示：

请注意，在某些语言（如 Java）中，没有无符号整数类型。在这种情况下，输入和输出都将被指定为有符号整数类型，并且不应影响您的实现，因为无论整数是有符号的还是无符号的，其内部的二进制表示形式都是相同的。
在 Java 中，编译器使用 二进制补码 记法来表示有符号整数。因此，在上面的 示例 3 中，输入表示有符号整数 -3。
 

示例 1：
```
输入：n = 11 (控制台输入 00000000000000000000000000001011)
输出：3
```
解释：输入的二进制串 00000000000000000000000000001011 中，共有三位为 '1'。
示例 2：
```
输入：n = 128 (控制台输入 00000000000000000000000010000000)
输出：1
```
解释：输入的二进制串 00000000000000000000000010000000 中，共有一位为 '1'。
示例 3：
```
输入：n = 4294967293 (控制台输入 11111111111111111111111111111101，部分语言中 n = -3）
输出：31
```
解释：输入的二进制串 11111111111111111111111111111101 中，共有 31 位为 '1'。
 

提示：

输入必须是长度为 32 的 二进制串 。

链接：https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/

解法一：

```Java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int count = 0;
        while (n!=0){
            count += n&1;
            n >>>=1;
        }
        return count;
    }
}
```

## 剑指 Offer 65. 不用加减乘除做加法
写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。

 

示例:
```
输入: a = 1, b = 1
输出: 2
```

提示：

a, b 均可能是负数或 0
结果不会溢出 32 位整数

链接：https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/


解法一：位运算

```Java
class Solution {
    public int add(int a, int b) {
        while(b != 0) { // 当进位为 0 时跳出
            int c = (a & b) << 1;  // c = 进位
            a ^= b; // a = 非进位和
            b = c; // b = 进位
        }
        return a;
    }
}

作者：jyd
链接：https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/solution/mian-shi-ti-65-bu-yong-jia-jian-cheng-chu-zuo-ji-7/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

```