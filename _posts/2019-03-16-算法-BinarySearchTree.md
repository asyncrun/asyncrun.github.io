---
layout: post
title: 二分查找
categories: [算法]
description: 二分查找递归、迭代实现
keywords: 二分查找
---

# 二分查找

```cpp
#include <iostream>
using namespace std;

/*Binary Search*/
int binarySearchRecursive(int arr[], int l, int r, int x)
{
	if (l <= r)
	{
		const auto mid = l + (r - l) / 2;
		if (arr[mid] == x)
		{
			return mid;
		}

		if (arr[mid] > x)
		{
			return binarySearchRecursive(arr, l, mid - 1, x);
		}

		return binarySearchRecursive(arr, mid + 1, r, x);
	}

	return -1;
}

int binarySearchIterative(const int arr[], int l, int r, int x)
{
	while (l <= r)
	{
		const auto mid = l + (r - l) / 2;
		if (arr[mid] == x) return mid;
		if (arr[mid] < x) return l = mid + 1;
		if (arr[mid] > x) return r = mid - 1;
	}

	return  -1;
}

/************************************************************************* 
 * Variants of Binary Search
 * https://www.geeksforgeeks.org/variants-of-binary-search/
 *************************************************************************/
int n = 8;
int a[] = { 2, 3, 3, 5, 5, 5, 6, 6 };

/*************************************************************************
Variant 1: Contains key (True or False)
Input : 2 3 3 5 5 5 6 6
Function : Contains(4)
Returns : False

Function : Contains(5)
Returns : True 
*************************************************************************/
bool contains(int low, int high, int key)
{
	auto ans = false;
	while (low <= high)
	{
		const auto mid = low + (high - low) / 2;
		const auto mid_val = a[mid];

		if (mid_val == key)
		{
			ans = true;
			break;
		}

		if (mid_val < key)
		{
			low = mid + 1;
		}
		else if (mid_val > key)
		{
			high = mid - 1;
		}
	}

	return ans;
}


/*************************************************************************
Variant 2: First occurrence of key (index of array). This is similar to
std::lower_bound(...)

Input : 2 3 3 5 5 5 6 6
Function : first(3)
Returns : 1

Function : first(5)
Returns : 3

Function : first(4)
Returns : -1
*************************************************************************/
int first(int low, int high, int key)
{
	auto ans = -1;
	while (low <= high)
	{
		const auto mid = low + (high - low) / 2;
		const auto mid_val = a[mid];

		if (mid_val == key)
		{
			ans = mid;
			high = mid - 1;
		}

		if (mid_val < key)
		{
			low = mid + 1;
		}
		else if (mid_val > key)
		{
			high = mid - 1;
		}
	}

	return ans;
}


/*************************************************************************
Variant 3: Last occurrence of key (index of array)
Input : 2 3 3 5 5 5 6 6
Function : last(3)
Returns : 2

Function : last(5)
Returns : 5

Function : last(4)
Returns : -1
*************************************************************************/
int last(int low, int high, int key)
{
	auto ans = -1;
	while (low <= high)
	{
		const auto mid = low + (high - low) / 2;
		const auto mid_val = a[mid];

		if (mid_val == key)
		{
			ans = mid;
			low = mid + 1;
		}

		if (mid_val < key)
		{
			low = mid + 1;
		}
		else if (mid_val > key)
		{
			high = mid - 1;
		}
	}

	return ans;
}

/*************************************************************************
Variant 4: index(first occurrence) of least integer greater than key.
This is similar to 
std::upper_bound(...)

Input : 2 3 3 5 5 5 6 6
Function : leastGreater(2)
Returns : 1

Function : leastGreater(5)
Returns : 6
*************************************************************************/
int leastgreater(int low, int high, int key)
{
	auto ans = -1;
	while (low <= high)
	{
		const auto mid = low + (high - low) / 2;
		const auto mid_val = a[mid];

		if (mid_val == key)
		{
			low = mid + 1;
		}

		if (mid_val < key)
		{
			low = mid + 1;
		}
		else if (mid_val > key)
		{
			ans = mid;
			high = mid - 1;
		}
	}

	return ans;
}

/*************************************************************************
Variant 5: index(first occurrence) of greatest integer lesser than key
Input : 2 3 3 5 5 5 6 6
Function : greatestLesser(2)
Returns : -1

Function : greatestLesser(5)
Returns : 2
*************************************************************************/
int greatestlesser(int low, int high, int key)
{
	auto ans = -1;
	while (low <= high)
	{
		const auto mid = low + (high - low) / 2;
		const auto mid_val = a[mid];

		if (mid_val == key)
		{
			high = mid - 1;
		}

		if (mid_val < key)
		{
			ans = mid;
			low = mid + 1;
		}
		else if (mid_val > key)
		{
			high = mid - 1;
		}
	}

	return ans;
}

/************************************************************************/
int main()
{
	printf("Contains\n");
	for (int i = 0; i < 10; i++)
	{
		printf("%d %d\n", i, contains(0, n - 1, i));
	}

	printf("First occurence of key\n");
	for (int i = 0; i < 10; i++)
	{
		printf("%d %d\n", i, first(0, n - 1, i));
	}

	printf("Last occurence of key\n");
	for (int i = 0; i < 10; i++)
	{
		printf("%d %d\n", i, last(0, n - 1, i));
	}

	printf("Least integer greater than key\n");
	for (int i = 0; i < 10; i++)
	{
		printf("%d %d\n", i, leastgreater(0, n - 1, i));
	}

	printf("Greatest integer lesser than key\n");
	for (int i = 0; i < 10; i++)
	{
		printf("%d %d\n", i, greatestlesser(0, n - 1, i));
	}
		
	return 0;
}
```