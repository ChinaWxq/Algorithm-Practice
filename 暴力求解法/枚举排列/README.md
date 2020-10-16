# 枚举排列

## 1 ~ n的字典序排列

利用递归的思想，先生成1的排列，直到n的排列。
print_permutation(序列 A, 集合 S)。
A为已排序列，S为剩余元素集合。

- 如果S集合为空，输出A序列。
- 如果S集合不为空，将S按序的第一个元素加入序列A，调用自身进行递归。

```cpp
#include <cstdio>
#include <vector>
#include <algorithm>
using namespace std;
void print_permutation(int n, int *A, int cur) {
	if (cur == n) { // 递归边界
		for (int i = 0; i < n; ++i) {
			printf("%d ", A[i]);
		}
		printf("\n");
	}
	else {
		for (int i = 1; i <= n; ++i) { // 尝试在A[cur]中填数
			int ok = 1;
			for (int j = 0; j < cur; ++j) { // 查找未使用数字
				if (i == A[j]) {
					ok = 0;
					break;
				}
			}
			if (ok) {
				A[cur] = i; // 插入
				print_permutation(n, A, cur+1);
			} 
		}
	}
}
int main() {
	int A[10];
	print_permutation(5, A, 0);
	return 0;
}
```

## STL下一个排列

```cpp
#include <cstdio>
#include <vector>
#include <algorithm>
using namespace std;
int main() {
	int n, p[10];
	scanf("%d", &n);
	for (int i = 0; i < n; ++i) {
		scanf("%d", &p[i]);
	}
	sort(p, p+n);
	do {
		for (int i = 0; i < n; ++i) {
			printf("%d ", p[i]);
		}
		printf("\n");
	} while (next_permutation(p, p+n));
	return 0;
}
```

