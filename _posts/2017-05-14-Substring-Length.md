---
layout: post
comments: true
title: 求最长公共子串长度
date: 2017-05-14
10 categories: blog
tags: [动态规划]
---

动态规划在程序中有时候非常有用，这里通过一个LCS问题来简单介绍下Dynamic Program。

> LCS(Longest Common Subsequence)问题：给定两个字符串，从中分别选取几个字符按原来的顺序组成新的字符串且这两个刚好相同，叫做CS(Common Subsequence)，其中最长的叫做LCS.

开始分析问题。

首先假设两个字符串s1和s2的长度分别为m和n，其中s1一共有$2^m$个子串，s2共有$2^n$个子串，所以如果使用暴力穷举的话时间复杂度为$O(2^{m+n})$，显然这不是一个令人满意的答案。下面介绍一种通过动态规划思想进行优化过的算法能够将时间复杂度降到$O(m*n)$。

首先我们用$record[i,j]$表示$s1[1:i]$和$s2[1:j]$的最长公共子串长度，现在我们已知$record[i-1,j]$和$record[i,j-1]$以及$record[i-1,j-1]$，现在要求$record[i,j]$。如果$s1[i]=s2[j]$的话，显然$record[i,j]=record[i-1,j-1]+1≥max(record[i-1,j],record[i,j-1])$，所以这时候$record[i,j]=record[i-1,j-1]+1$。否则$record[i,j]=max(record[i-1,j],record[i,j-1])$。

下面是伪代码:

```
function LCS(s1,s2,i,j):
	if s1[i] = s2[j]:
		return record[i-1,j-1]+1;
	else:
		return max(record[i-1,j],record[i,j-1]);
```

当你把这个式子写成递归树的话，发现最后树的深度达到了$2^{m+n}$，因为其中有很多重复的子树，我们可以采用备忘录的方法将每次计算出的值进行记录，那么由于我们只记录$record[1:m,1:n]$，所以最后的时间复杂度为$O(m*n)$。

上面的方法是通过递归从顶层往底层计算的，但如果我们将递归转为循环直接自底向上进行推演，其实能够比上面的方法更快，至少减少了函数调用的资源消耗。下面是代码:

```
int LCS(string& s1, string& s2)
{
	vector < vector<int>> record = vector<vector<int>>(s1.size()+1, vector<int>(s2.size()+1, 0));
	for (int i = 1; i <= s1.size(); ++i) {
		for (int j = 1; j <= s2.size(); ++j) {
			if (s1[i] == s2[j])record[i][j] = record[i - 1][j - 1] + 1;
			else record[i][j] = max(record[i - 1][j], record[i][j - 1]);
		}
	}
	return record[s1.size()][s2.size()];
}
```

代码很短，但能够求出答案，最终的时间复杂度为$O(m*n)$。

下面附上MIT算法导论课的照片，希望能够加深理解:

![](https://raw.githubusercontent.com/dogloving/dogloving.github.io/master/img/20170514/pic3.png)

通过这张图，我们可以找到所有的公共子串。

下面的两张图能够充分体现MIT自由活泼的课堂文化:

![](https://raw.githubusercontent.com/dogloving/dogloving.github.io/master/img/20170514/pic1.jpg)

![](https://raw.githubusercontent.com/dogloving/dogloving.github.io/master/img/20170514/pic2.jpg)