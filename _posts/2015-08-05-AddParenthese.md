---

layout: post

title: "学习Java Servlet&JSP Nuts and Bolts"

data: 2015-08-05

categories: jekyll update

---

```
<link rel="stylesheet" href="/stylesheets/highlightstyles/default.css">

<script src="/javascripts/highlight.pack.js"></script>

<script>hljs.initHighlightingOnLoad();</script>
```

```
<pre><code class="java">
public class AddParenthese {
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
```