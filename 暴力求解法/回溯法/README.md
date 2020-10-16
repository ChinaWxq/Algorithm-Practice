# 回溯法

递归函数不再递归调用它自身，而是返回上一层调用，这种现象称为回溯。在递归构造中，生成和检查过程可以有机结合起来。

## 八皇后

最简单的思路是将问题转化为64个格子选一个大小为8的子集，64个格子的子集是2<sup>64</sup>个，太大了。

第二个思路是64个各种选8个格子，组合生成问题，C<sub>64</sub><sup>8</sup>=4.426*10<sup>9</sup>种方案，比第一种好但仍不够优秀。

我们发现每行每列只放置一个皇后，如果用a[x]表示第x行的皇后列编号，就把问题变成了全排列问题，0~7的排列一共有8!=40320个，枚举数量不会超过他。

- 枚举尝试把当前皇后在i列
- 检查是否与之前的皇后冲突，如果冲突回溯
- 否则继续递归下一行皇后

```cpp
#include <cstdio>
using namespace std;
int tot = 0;
int n = 8;
int a[10];
void search(int cur) {
	if (cur == n) { // 递归边界
		tot++;
	}
	else {
		for (int i = 0; i < n; ++i) {
			int ok = 1;
			a[cur] = i; // 尝试把第cur行的皇后放在i列
			for (int j = 0; j < cur; ++j) { // 检查是否与之前的皇后冲突
				if (a[cur] == a[j] || cur - a[cur] == j - a[j] || j + a[j] == cur + a[cur]) {
					ok = 0;
					break;
				}
			}
			if (ok) {
				search(cur+1); // 合法继续递归
			}
		}
	}
}
int main() {
	search(0);
	printf("8皇后的总方案数: %d\n", tot);
	return 0;
}
```

既然是逐行放置的，皇后横向不会冲突，只需要检查纵向或者斜向。

`cur - a[cur] == j - a[j]`来判断(cur, a[cur])和(j, a[j])是否在主对角线上。

`cur + a[cur] == j + a[j]`来判断(cur, a[cur])和(j, a[j])是否在副对角线上。

