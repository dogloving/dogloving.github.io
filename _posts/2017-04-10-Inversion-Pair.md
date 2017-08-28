---
layout: post
comments: true
title: 求逆序对
date: 2017-04-10
10 categories: blog
tags: [记录]
---

在线性代数中有学到过逆序对，关于逆序对的定义如下:

> 如果存在正整数 i, j 使得 1 ≤ i ＜ j ≤ n 而且 A[i] ＞ A[j]，则 <A[i], A[j]> 这一个[有序对](https://zh.wikipedia.org/wiki/%E6%9C%89%E5%BA%8F%E5%AF%B9)称为 A 的一个**逆序对**，也称作逆序。逆序对的数量称作逆序数。

假设我们现在有一组随机排列，我们要求每个元素的逆序对数。如果使用双重循环暴力求解时间复杂度为O(n^2)，不过这样显然不够优雅。现在有一种O(nlogn)的解法，我觉得很优雅并且不禁感叹“他们是怎么想到的"，所以决定记录下来以便日后再看。

先上代码:

```
#include <iostream>
#include <vector>
#include <utility>
using namespace std;
void mergeCount(vector<pair<int,int>>& nums, vector<int>& count, int left1, int right1,int left2,int right2) {
	vector<pair<int,int>> tmp(right1-left1+right2-left2+2, make_pair(0,0));
	int point = 0;
	int current1 = left1, current2 = left2;
	while (current1 <= right1 && current2 <= right2) {
		if (nums[current1].first < nums[current2].first) {
			tmp[point++] = nums[current1];
			count[nums[current1].second] += current2 - left2;
			++current1;
		}
		else {
			tmp[point++] = nums[current2++];
		}
	}
	while (current1 <= right1) {
		tmp[point++] = nums[current1];
		count[nums[current1++].second] += (current2 - left2);
	}
	while (current2 <= right2) {
		tmp[point++] = nums[current2++];
	}
	point = 0;
	for (int i = left1; i <= right2; ++i) {
		nums[i] = tmp[point++];
	}
}
void sortCount(vector<pair<int,int>>& nums, vector<int>& count,int left,int right) {
	if (left >= right)return;
	int mid = left + (right - left) / 2;
	int left1 = left, right1 = mid, left2 = mid + 1, right2 = right;
	sortCount(nums, count, left2, right2);
	sortCount(nums, count, left1, right1);
	mergeCount(nums, count, left1, right1, left2, right2);
}
int main()
{
	vector<pair<int,int>> nums;
	vector<int> count;
	int n;
	cin >> n;
	int nn = n;
	int i = 0;
	while (n--) {
		int x;
		cin >> x;
		nums.push_back(make_pair(x,i++));
		count.push_back(0);
	}
	sortCount(nums, count, 0, nn - 1);
	for (auto i : count)
		cout << i << ' ';
	cout << endl;
	system("pause");
}
```

代码的思路是这样的：

```
假设我们已经有两组数组，已经分别求出他们中的每个元素在其数组中的逆序对数并且已经对他们分别排好序了，现在我们需要将他们进行合并然后求出新的数组中的每个元素的逆序对数。将问题转化成这样以后比之前的容易多了。我们需要用到归并排序中的方法，用两个指针分别指向两个数组，然后取指针指向的较小的元素放到新的数组中，然后对应的指针往前移一位。这个操作不只是将两个数组归并，还有一个作用是求出了某个数组中的某个元素在另一个数组中能排在第几位，这个就能找出此数组中某个元素与另一个数组中的元素能组成几对逆序对。
有了上面的结论我们可以反向来求每个元素的逆序对数，需要注意的是进行排序之后我们需要将原先的index放到正确的位置，所以我这里用了pair来存储每个元素，pair.first存储值，pair.second存储index，然后计算count的时候就使用pair.second。
```

关于这个算法的时间复杂度：

```
由于T(n) = T(n/2) + T(n/2) + cn，所以最终得出T(n) = O(nlogn)
```

