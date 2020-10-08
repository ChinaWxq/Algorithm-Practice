
[POJ-2456](https://vjudge.net/problem/POJ-2456)

在n个点中选c个点使得相邻的点之间的最小距离最大，求其最大值。

求二分区间中满足条件的最大值。

二分区间为（0，数组中最大差距），如果mid满足题意那么比mid小的答案也满足题意。
```cpp
#include <cstdio>
#include <algorithm>
using namespace std;
const int MAXN = 1e5 + 10;
int a[MAXN];
int n, c;
bool check(int mid) {
	int x = a[0];
	int num = 1;
	for (int i = 1; i < n && num < c; ++i) {
		if (a[i] - x >= mid) {
			num++;
			x = a[i];
		}
	}
	return num == c ? true : false;
}
int main() {
	while (~scanf("%d%d", &n, &c)) {
		int minNum = 2e9;
		int maxNum = 0;
		for (int i = 0; i < n; ++i) {
			scanf("%d", &a[i]);
			minNum = min(minNum, a[i]);
			maxNum = max(maxNum, a[i]);
		}
		sort(a, a + n);
		int l = 0;
		int r = maxNum - minNum;
		int ans = 0;
		while (l <= r) {
			int mid = (l + r) >> 1;
			if (check(mid)) {
				ans = mid;
				l = mid + 1;
			} else {
				r = mid - 1;
			}
		}
		printf("%d\n", ans);
	}	
	return 0;
}```
