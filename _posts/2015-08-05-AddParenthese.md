---

layout: post

title: "[LeetCode] Add Parentheses"

data: 2015-08-05

categories: jekyll update

---


<link rel="stylesheet" href="/stylesheets/highlightstyles/default.css">

<script src="/javascripts/highlight.pack.js"></script>

<script>hljs.initHighlightingOnLoad();</script>

### 算法分析

题目要求是构建所有`添加括号`的办法，最后返回所有计算结果。
注意是添加括号的办法。

很容易想到的办法是利用分治的办法递归地解决办法。而怎么划分子问题是最关键的问题。

我首先想到的办法是两两合并运算数，但是最后实际是错误的。因为两两合并造成一个重大的问题：添加括号的办法实际是有重复出现的（比如前后独立合并时候，前后两次递归全都算过）

我一开始想通过改进来解决这个问题，未遂。

所以我转而学习别人的解决思路。

划分子问题：用运算符将一个input String拆分。这样两边分而治之，且每种划分（顺序遍历所有的运算符）得到的括号分布是不可能相同的。

解决子问题：对于每个input String，根据运算符划分成两个小规模input，分别得到两个input计算得到的`list`以后，利用划分时的运算符计算出所有结果。

结束条件：此处的input无法划分，查找运算符的`for`循环没有实际内容，导致`result`中结果为空。

### 启示

1. 不要贸然构建数据结构，可能是多余的，可以直接input String分析
2. java中的switch，初始化要求等语法

### 源代码

<pre><code class="java">public class AddParenthese {
    public List<Integer> diffWaysToCompute(String input) {
        List<Integer> results = new ArrayList<Integer>();
        for(int i=0; i<input.length(); i++) {
            if(input.charAt(i) == '-'
                    || input.charAt(i) == '+'
                    || input.charAt(i) == '*') { 
                String frontStr = input.substring(0, i);
                String backStr = input.substring(i+1, input.length());

                List<Integer> frontResults = diffWaysToCompute(frontStr);
                List<Integer> backResults = diffWaysToCompute(backStr);

                //-!- 学习这里的循环单位定义
                for(Integer f: frontResults) {              
                    for(Integer b: backResults) {
                        //-!- 被使用的变量必须被初始化过，否则报错 
                        int c = 0;
                        switch(input.charAt(i)) {
                            case '+':
                                c = f + b;
                                break;
                            case '-':
                                c = f - b;
                                break;
                            case '*':
                                c = f * b;
                                break;
                        }
                        results.add(c);
                    }
                }
            }
        }
        //-!- End Point in Divide-and-Conquar
        if(results.size() == 0)
            results.add(Integer.valueOf(input));
        
        return results;
    }
}
</code></pre>