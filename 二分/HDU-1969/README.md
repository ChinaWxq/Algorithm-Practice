[HDU-1969](https://vjudge.net/problem/HDU-1969)

将n个半径为a[i]的馅饼分给f+1个人，每个人分到的馅饼体积一样，求每个人能获取馅饼体积的最大值。

求二分区间满足条件的最大值。

注意浮点二分，更新区间控制精度且不能加1。

```cpp
#include <cstdio>
#include <algorithm>
#include <cmath>
using namespace std;
const int MAXN = 1e4 + 10;
const double eps = 1e-10;// 精确度
const double pi = 4*atan(1.0); // 2π
int n, f;
double a[MAXN];
bool check(double mid) {
	double s = mid * mid;
	int num = 0;
	for (int i = 0; i < n; ++i) {
		double tmp = a[i] * a[i];
		num += int(tmp / s);
	}
	return num >= f + 1 ? true : false;
}
int main() {
	int t;
	scanf("%d", &t);
	while (t--) {
		scanf("%d%d", &n, &f);
		for (int i = 0; i < n; ++i) {
			scanf("%lf", &a[i]);
		}
		double l = 0;
		double r = 10000.0;
		double ans = 0;
		while (fabs(r - l) > eps) {
			double mid = (l + r) / 2.0;
			if (check(mid)) {
				ans = mid;
				l = mid;
			} else {
				r = mid;
			}
		}
		printf("%.4lf\n", ans * ans * pi);
	}
	return 0;
}
```