## 冒泡排序
> 思路：让数组中的元素像水中的气泡一样上浮，进而达到排序的目的。

- 重复以下步骤，直到数组中不包含顺序相反的相邻元素
1. 从数组末尾开始依次比较相邻两个元素，如果大小关系相反则交换位置

### 复杂度分析
时间复杂度：O(n<sup>2</sup>)
空间复杂度：O(1)

冒泡排序进交换数组中的相邻元素进行比较和交换，因此不会改变元素的相对位置，是一种<font color="red">稳定的排序算法</font>。
冒泡排序中的交换次数称为反序数或逆序数，用于体现数列的错乱程度。


```cpp
#include <iostream>
using namespace std;

int bubbleSort(int a[], int n) {
	int sw = 0;
	bool flag = 1;
	for (int i = 0; flag; ++i) {
		flag = 0;
		for (int j = n - 1; j >= i + 1; --j) {
			if (a[j] < a[j-1]) {
				swap(a[j], a[j-1]);
				flag = 1;
				sw++;
			}
		}
	}
	return sw;
}

int main() {
	int a[100], n, sw;
	cin >> n;

	for (int i = 0; i < n; ++i) {
		cin >> a[i];
	}

	sw = bubbleSort(a, n);

	for (int i = 0; i < n; ++i) {
		if (i) {
			cout << " ";
		}
		cout << a[i];
	}
	cout << endl << sw << endl;

	return 0;
}
```