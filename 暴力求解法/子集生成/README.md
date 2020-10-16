# 子集生成

## 位向量法

用B[i] = 1，表示选第i个元素。只有当所有的元素是否被选择确定后才是一个完整的子集。这是一棵n+1层的二叉树，cur的范围从0~n。

```cpp
#include <cstdio>
using namespace std;
void print_subset(int n, int *B, int cur) {
	if (n == cur) {
		// 打印集合
		for (int i = 0; i < n; ++i) {
			if (B[i]) {
				printf("%d ", i);
			}
		}
		printf("\n");
		return ;
	}
	// 选第cur个元素
	B[cur] = 1;
	print_subset(n, B, cur+1);
	// 不选第cur个元素
	B[cur] = 0; 
	print_subset(n, B, cur+1);
}
int main() {
	int B[10] = {0};
	print_subset(3, B, 0);
}

// 输出
0 1 2 
0 1 
0 2 
0 
1 2 
1 
2 
```

## 二进制法

用二进制来表示子集{0, 1, 2, 3, ..., n-1}，从右往左第i位表示元素i是否在集合S中。

```cpp
void print_subset(int n, int s) {
	for (int i = 0; i < n; ++i) {
		if (s & (1 << i)) {
			printf("%d ", i);
		}
	}
	printf("\n");
}
int main() {
	int n = 5;
	for (int i = 0; i < (1 << n); ++i) {
		print_subset(n, i);
	}
}
```

