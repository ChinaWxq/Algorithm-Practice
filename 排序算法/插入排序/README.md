## 插入排序
> 思路：打扑克牌时排列手牌的方法相似。将牌从左到右，从大到小排序。我们需要将牌抽出来插入到已经排好序的手牌中的合适位置，重复插入过程完成排序。

核心思想：向有序序列中插入元素。

- 将首元素视为已排序序列
- 执行下列过程直至未排序部分消失
1. 取出未排序部分的首元素赋给tmp
2. 在已排序部分，将所有比tmp大的元素向后移动一个单位
3. 将tmp插入到合适的空位

### 复杂度分析
时间复杂度：O(n<sup>2</sup>)
空间复杂度：O(1)

在插入排序中，我们将比tmp大的元素向后移动，不相邻的元素不会交换相对位置，因此插入排序算法是<font color = red>稳定的</font>。

```cpp
#include <stdio.h>

// log输出
void trace(int a[], int n) {
	int i;
	for (i = 0; i < n; ++i) {
		if (i > 0) printf(" ");
		printf("%d", a[i]);
	}
	printf("\n");
}

// 插入排序
void insertionSort(int a[], int n) {
	int i, j, tmp;
	for (i = 1; i < n; ++i) {
		j = i - 1;
		tmp = a[i];
		while (j >= 0 && a[j] > tmp) {
			a[j + 1] = a[j];
			j--;
		}
		a[j+1] = tmp;
		trace(a, n);
	}
}

int main() {
	int n, i;
	int a[100];

	scanf("%d", &n);

	for (i = 0; i < n; ++i) {
		scanf("%d", &a[i]);
	}

	trace(a, n);
	insertionSort(a, n);

	return 0;
}
```