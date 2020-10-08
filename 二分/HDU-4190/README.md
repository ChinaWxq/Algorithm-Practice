[HDU-4190](https://vjudge.net/problem/HDU-4190)

把b个投票箱分配到n个城市，每个城市至少一个投票箱，每个投票箱的容量相同，投票箱的容量最小是多少？

求二分区间中满足条件的最小值。

```cpp
#include <cstdio>
#include <algorithm>
#include <cmath>
using namespace std;
const int MAXN = 5e5 + 10;
int a[MAXN];
int n, b;
bool check(int mid) {
	int num = 0;
	for (int i = 0; i < n; ++i) {
		num += (int)ceil(a[i] * 1.0 / mid);
	}
	if (num <= b) {
		return true;
	} else {
		return false;
	}
}
int main() {
	while (~scanf("%d%d", &n, &b)) {
		if (n == -1 && b == -1) {
			break;
		}
		for (int i = 0; i < n; ++i) {
			scanf("%d", &a[i]);
		}
		int l = 0;
		int r = 2e9;
		int ans = 0;
		while (l <= r) {
			int mid = (l + r) >> 1;
			if (check(mid)) {
				ans = mid;
				r = mid - 1;
			} else {
				l = mid + 1;
			}
		}
		printf("%d\n", ans);
	}
}
```