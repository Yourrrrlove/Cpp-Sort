# 排序

## 插入排序

### 直接插入排序

```c++
#include<iostream>
#include<string>
using namespace std;

void InsertSort(int* ls, int len)
{
	int i, j;
	for (i = 2; i < len; i++)
	{
		if (ls[i] < ls[i - 1])
		{
			ls[0] = ls[i];
			for (j = i - 1; ls[0] < ls[j]; j--)
			{
				ls[j + 1] = ls[j];
			}
			ls[j + 1] = ls[0];
		}
	}
	for (i = 1; i < len; i++)
	{
		cout << ls[i] << " ";
	}
	cout << endl;
}
int main()
{
	int ls[] = { 0, 1, 3, 5, 7, 9, 4, 8, 11 };
	int len = sizeof(ls) / sizeof(ls[0]);
	InsertSort(ls, len);
	int i;
	for (i = 1; i < sizeof(ls) / sizeof(ls[0]); i++)
	{
		cout << ls[i] << " ";
	}
	cout << endl;
	system("pause");
	return 0;
}
```

### 折半插入排序

```c++
#include<iostream>
#include<string>
using namespace std;

void InsertSort(int* ls, int len)
{
	int i, j;
	for (i = 2; i < len; i++)
	{
		ls[0] = ls[i];
		int left = 1;
		int right = i - 1;
		int mid = 0;
		while (left <= right)
		{
			mid = (left + right) / 2;
			if (ls[0] < ls[mid])
			{
				right = mid - 1;
			}
			else
			{
				left = mid + 1;
			}
		}
		for (j = i - 1; j >= right + 1; j--)
		{
			ls[j + 1] = ls[j];
		}
		ls[right + 1] = ls[0];
	}
	for (i = 1; i < len; i++)
	{
		cout << ls[i] << " ";
	}
	cout << endl;
}
int main()
{
	int ls[] = { 0, 1, 3, 5, 7, 9, 4, 8, 11 };
	int len = sizeof(ls) / sizeof(ls[0]);
	InsertSort(ls, len);
	int i;
	for (i = 1; i < sizeof(ls) / sizeof(ls[0]); i++)
	{
		cout << ls[i] << " ";
	}
	cout << endl;
	system("pause");
	return 0;
}
```

#### 折半插入排序算法分析

- 。减少了比较次数，但没有减少移动次数。
- 平均性能优于直接插入排序
- 时间复杂度为 O(n^2)
- 空间复杂度为 O(1)
- 是一种稳定的排序方法

### 希尔排序

先将整个待排记录序列分割成若干子序列，分别进行直接插入排序，待整个序列中的记录"基本有序时，再对全体记录进行一次直接插入排序。

希尔排序是不稳定的。

![image-20231001200053833](https://article.biliimg.com/bfs/article/d4b4c22c4fd0d941a09f1dd16b6f042c488897681.png)

```c++
#include<iostream>
#include<string>
using namespace std;
void ShellInsert(int* ls, int dk, int len)
{
	int i, j;
	for (i = dk + 1; i < len; i++)
	{
		if (ls[i] < ls[i - dk])
		{
			ls[0] = ls[i];
			for (j = i - dk; j>0 && (ls[0] < ls[j]); j-=dk)
			{
				ls[j + dk] = ls[j];
			}
			ls[j + dk] = ls[0];
		}
	}
}
void Sort(int* ls, int* dlta, int t, int len)
{
	int i, k;
	for (k = 0; k < t; k++)
	{
		ShellInsert(ls, dlta[k], len);
	}
	for (i = 1; i < len; i++)
	{
		cout << ls[i] << " ";
	}
	cout << endl;
}
int main()
{
	int ls[] = { 0, 1, 3, 5, 7, 9, 4, 8, 11, 41, 28, 20, 50, 45, 40, 30, 55, 60};
	int dlta[] = { 5,3,1 };
	int t = 3;
	int len = sizeof(ls) / sizeof(ls[0]);
	Sort(ls, dlta, t, len);
	int i;
	for (i = 1; i < len; i++)
	{
		cout << ls[i] << " ";
	}
	cout << endl;
	system("pause");
	return 0;
}
```

## 交换排序

### 冒泡排序

列表中有 n 个元素，需要比较 n-1 趟；第 i 趟需要比较 n-i 次。

```c++
#include<iostream>
#include<string>
using namespace std;

void BubbleSort(int* ls, int len)
{
	int i, j, temp;
	for (i = 1; i < len; i++)
	{
		for (j = 1; j < len - i; j++)
		{
			if (ls[j] > ls[j + 1])
			{
				temp = ls[j];
				ls[j] = ls[j + 1];
				ls[j + 1] = temp;
			}
		}
	}
	for (i = 1; i < len; i++)
	{
		cout << ls[i] << " ";
	}
	cout << endl;
}
int main()
{
	int ls[] = { 0, 1, 3, 5, 7, 9, 4, 8, 11, 41, 28, 20, 50, 45, 40, 30, 55, 60};
	int len = sizeof(ls) / sizeof(ls[0]);
	BubbleSort(ls, len);
	int i;
	for (i = 1; i < len; i++)
	{
		cout << ls[i] << " ";
	}
	cout << endl;
	system("pause");
	return 0;
}
```

改进版本冒泡排序，设置 flag作为是否需要交换的标志：

```c++
#include<iostream>
#include<string>
using namespace std;

void BubbleSort(int* ls, int len)
{
	int i, j, temp;
	int flag = 1;  //flag=1意味着本趟需要进行交换
	for (i = 1; i < len && flag == 1; i++)
	{
		flag = 0;
		for (j = 1; j < len - i; j++)
		{
			if (ls[j] > ls[j + 1])
			{
				flag = 1;
				temp = ls[j];
				ls[j] = ls[j + 1];
				ls[j + 1] = temp;
			}
		}
		cout << "flag = " << flag << endl;
	}
	for (i = 1; i < len; i++)
	{
		cout << ls[i] << " ";
	}
	cout << endl;
	
}
int main()
{
	int ls[] = { 0, 1, 3, 5, 7, 9, 4, 8, 11, 41, 28, 20, 50, 45, 40, 30, 55, 60};
	int len = sizeof(ls) / sizeof(ls[0]);
	BubbleSort(ls, len);
	int i;
	for (i = 1; i < len; i++)
	{
		cout << ls[i] << " ";
	}
	cout << endl;
	system("pause");
	return 0;
}
```

### 快速排序

- 任取一个元素（如：第一个）为中心
- 所有比它\的元素一律前放，比它大的元素一律后放，开成左右两个子表
- 对各子表重新选择中心元素并依此规则调整
- 直到每个子表的元素只剩一个

```c++
#include<iostream>
#include<string>
using namespace std;

int Partition(int* ls, int low, int high)
{
	int piv_value;
	ls[0] = ls[low];
	piv_value = ls[low];
	while (low < high)
	{
		while (low < high && ls[high] >= piv_value)
		{
			high--;
		}
		ls[low] = ls[high];
		while (low < high && ls[low] <= piv_value)
		{
			low++;
		}
		ls[high] = ls[low];
	}
	ls[low] = ls[0];
	return low;
}
void QSort(int* ls, int low, int high)
{
	if (low < high)
	{
		int pivot = Partition(ls, low, high);
		cout << "中心点为第 " << pivot << " 个元素" << endl;
		QSort(ls, low, pivot - 1);
		cout << "左半部分执行完毕" << endl;
		QSort(ls, pivot + 1, high);
		cout << "右半部分执行完毕" << endl;
	}
	
}
int main()
{
	int ls[] = { 0, 49, 38, 65, 97, 76, 13, 27, 49};
	int len = sizeof(ls) / sizeof(ls[0]);
	QSort(ls, 1, len-1);
	int i;
	for (i = 1; i < len; i++)
	{
		cout << ls[i] << " ";
	}
	cout << endl;
	system("pause");
	return 0;
}
```

## 选择排序

### 简单选择排序

简单选择排序==不需要==第 0 号位置当==哨兵==

是不稳定排序

时间复杂度：O(n^2)

空间复杂度：O(1)

```c++
#include<iostream>
#include<string>
using namespace std;

void Swap(int& a, int& b)
{
	int temp = a;
	a = b;
	b = temp;
}
void SelectSort(int* ls, int len)
{
	int i, j, k;
	for (i = 0; i < len-1; i++)
	{
		k = i;
		for (j = i + 1; j < len; j++)
		{
			if (ls[j] < ls[k])
			{
				k = j;
			}
		}
		if (k != i)
		{
			Swap(ls[i], ls[k]);
		}
	}
}
int main()
{
	int ls[] = { 0, 49, 38, 65, 97, 76, 13, 27, 49};
	int len = sizeof(ls) / sizeof(ls[0]);
	SelectSort(ls,len);
	int i;
	for (i = 0; i < len; i++)
	{
		cout << ls[i] << " ";
	}
	cout << endl;
	system("pause");
	return 0;
}
```

### 堆排序

大根堆、小根堆？

![image-20231002104623113](https://article.biliimg.com/bfs/article/a63648d3b74b746e559a34fd9a24e8b3488897681.png)

## 归并排序

2路归并排序：

![image-20231002104859060](https://article.biliimg.com/bfs/article/e8d46340db2dc80cc680bc086b24aa15488897681.png)

```c++
#include<iostream>
#include<string>
using namespace std;

void MergeSort(int* ls, int* lt, int low, int m, int high)
{
	int i = low, j = m + 1, k = 0;
	while (i <= m && j < high)
	{
		if (ls[i] <= ls[j])
		{
			lt[k++] = ls[i++];
		}
		else
		{
			lt[k++] = ls[j++];
		}
	}
	if (j >= high)
	{
		for (; k < high; k++,i++)
		{
			lt[k] = ls[i];
		}
	}
	if (i > m)
	{
		for (; j < high; j++, k++)
		{
			lt[k] = ls[j];
		}
	}
}
int main()
{
	int ls[] = { 10,20,30,0,7,15,25,28,35,40 };
	int len = sizeof(ls) / sizeof(ls[0]);
	int lt[10] = { 0 };  //lt的长度要修改
	MergeSort(ls,lt,0, 2, len);  //分界点m要修改
	int i;
	for (i = 0; i < len; i++)
	{
		cout << lt[i] << " ";
	}
	cout << endl;
	system("pause");
	return 0;
}
```



## 基数排序
