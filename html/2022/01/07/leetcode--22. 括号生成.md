# 22. 括号生成  
数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。

示例 1：

输入：n = 3
输出：["((()))","(()())","(())()","()(())","()()()"]
示例 2：

输入：n = 1
输出：["()"]

提示：

1 <= n <= 8

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/generate-parentheses  
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 解法
1.  暴力法  
递归生成字符串，然后判断加入结果List。
  
```Java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<String>();

        generateAll(new char[2*n],0,result);

        return result;
    }

    public void generateAll(char[] str,int pos,List<String> result){
        if (pos==str.length){
            if (valid(str)){
                result.add(new String(str));
            }
        }else{
            str[pos] = '(';
            generateAll(str, pos + 1, result);
            str[pos] = ')';
            generateAll(str, pos + 1, result);
        }
    }

    public boolean valid(char[] s){
        int n = 0;
        for(int i=0;i<s.length;i++){
            if (s[i]=='('){
                n++;
            }else if (s[i]==')'){
                n--;
            }
            if (n<0){
                return false;
            }
        }
        return n==0;
    }
}
```

2. 回溯法  
只在序列仍有效时添加括号  

```Java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> ans = new ArrayList<String>();
        backtrack(ans, new StringBuilder(), 0, 0, n);
        return ans;
    }

    public void backtrack(List<String> ans, StringBuilder cur, int open, int close, int max) {
        if (cur.length() == max * 2) {
            ans.add(cur.toString());
            return;
        }
        if (open < max) {
            cur.append('(');
            backtrack(ans, cur, open + 1, close, max);
            cur.deleteCharAt(cur.length() - 1);
        }
        if (close < open) {
            cur.append(')');
            backtrack(ans, cur, open, close + 1, max);
            cur.deleteCharAt(cur.length() - 1);
        }
    }
}

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/generate-parentheses/solution/gua-hao-sheng-cheng-by-leetcode-solution/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```
