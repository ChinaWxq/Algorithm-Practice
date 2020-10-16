[UVa 524](https://vjudge.net/problem/UVA-524)
输入正整数n，把整数1,2,3,4,...,n组成一个环，使相邻两个整数之和均为素数，输出时从整数1开始逆时针排列，同一个环应该输出1次，n<=16

```cpp
#include <cstdio>
#include <cmath>
#include <algorithm>
#include <cstring>
using namespace std;
const int MAXN = 50;
int pri[MAXN], a[MAXN], vis[MAXN], n;
bool isPrime(int n) {
	for (int i = 2; i <= sqrt(n); ++i) {
		if (n % i == 0) {
			return false;
		}
	}
	return true;
}
void dfs(int cur) {
	if (cur == n && pri[a[0] + a[n - 1]]) { // 递归边界
		for (int i = 0; i < n; ++i) {
			if (i) {
				printf(" ");
			}
			printf("%d", a[i]);
		}
		printf("\n");
		return ;
	} else {
		for (int i = 2; i <= n; ++i) { // 从2开始
			if (!vis[i] && pri[i + a[cur - 1]]) { // 没有被使用过，满足条件
				a[cur] = i;
				vis[i] = 1; // 设置标志
				dfs(cur + 1);
				vis[i] = 0; // 清除标志
			}
		}
	}
}
int main() {
	int cnt = 0;
	while (~scanf("%d", &n)) {
		if (cnt) {
			printf("\n");
		}
		memset(vis, 0, sizeof(vis));
		for (int i = 0; i <= 2 * n; ++i) {
			pri[i] = isPrime(i);
		}
		printf("Case %d:\n", ++cnt);
		a[0] = 1;
		dfs(1);
	}
	return 0;
}
```
