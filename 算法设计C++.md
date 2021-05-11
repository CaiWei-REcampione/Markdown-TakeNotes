

# 排序

## 冒泡算法	bubbleSort

```cpp
/// <summary>
/// sort vector from greater to less
/// </summary>
/// <typeparam name="T">typename</typeparam>
/// <param name="vec">vector parameter</param>
/// <returns>result vector</returns>
template<typename T>
vector<T>bubbleSort(vector<T>vec) {
	vector<T>res(vec);
	for (int i = 0; i < res.size(); i++) {
		for (int j = 0; j < res.size() - i - 1; j++) {
			if (res[j] < res[j + 1]) {
				swap(res[j], res[j + 1]);
			}
		}
	}
	return res;
}
```

## 选择排序	selectionSort

```cpp
/// <summary>
/// sort vector from greater to less
/// </summary>
/// <typeparam name="T">typename</typeparam>
/// <param name="vec">vector parameter</param>
/// <returns>result vector</returns>
template<typename T>
vector<T>selectionSort(vector<T>vec) {
	vector<T>res(vec);
	for (int i = 0; i < res.size(); i++) {
		size_t maxindex = i;
		for (int j = i + 1; j < res.size(); j++) {
			if (res[maxindex] < res[j]) {
				maxindex = j;
			}
		}
		swap(res[maxindex], res[i]);
	}
	return res;
}
```

## 插入排序	insertionSort

```cpp
/// <summary>
/// sort vector from greater to less
/// </summary>
/// <typeparam name="T">typename</typeparam>
/// <param name="vec">vector parameter</param>
/// <returns>result vector</returns>
template<typename T>
vector<T> insertionSort(vector<T> vec) {
	vector<T>res(vec);
	for (int i = 1; i < res.size(); i++) {
		T temp = res[i];
		int j;
		for (j = i - 1; j >= 0 and res[j] < temp; j--) {
			res[j + 1] = res[j];
		}
		res[j + 1] = temp;
	}
	return res;
}
```

## 快速排序	quickSort

```cpp
/// <summary>
/// sort vector from less to greater
/// </summary>
/// <typeparam name="T">typename</typeparam>
/// <param name="vec">vector parameter</param>
/// <returns>result vector</returns>
template<typename T>
vector<T>quickSort(vector<T> vec) {
	vector<T>res(vec);
	quickSort(res, 0, res.size() - 1);
	return res;
}
template<typename T>
void quickSort(vector<T>& vec, int left, int right) {
	int middle = vec[(left + right) / 2];
	int tleft = left, tright = right;
	while (tleft <= tright) {
		while (vec[tleft] < middle) {
			tleft++;
		}
		while (middle < vec[tright]) {
			tright--;
		}
		if (tleft <= tright) {
			swap(vec[tleft], vec[tright]);
			tleft++;
			tright--;
		}
	}
	if (tleft == tright) {
		tleft++;
	}
	if (left < tright) {
		quickSort(vec, left, tleft - 1);
	}
	if (tleft < right) {
		quickSort(vec, tright + 1, right);
	}
	return;
}
```

## sort函数

```cpp
/// <summary>
/// greater to lower
/// </summary>
/// <typeparam name="T">typename</typeparam>
/// <param name="a"></param>
/// <param name="b"></param>
/// <returns>
/// true: don't swap
/// false: swap
/// </returns>
template<typename T>
bool cmp(T a, T b) {
	if (a > b) {
		return true;
	}
	else {
		return false;
	}
}
```

```cpp
/// <summary>
/// lower to greater
/// </summary>
/// <typeparam name="T">typename</typeparam>
/// <param name="a"></param>
/// <param name="b"></param>
/// <returns>
/// true: don't swap
/// false: swap
/// </returns>
template<typename T>
bool cmp(T a, T b) {
	if (a < b) {
		return true;
	}
	else {
		return false;
	}
}
```



# 查找

## 二分法

```cpp
/// <summary>
/// binary search
/// </summary>
/// <typeparam name="T">typename</typeparam>
/// <param name="vec">vector</param>
/// <param name="target">search value</param>
/// <returns>find or not</returns>
template<typename T>
bool binarySearch(vector<T>vec, int target) {
	int left = 0, right = vec.size() - 1;
	while (left <= right) {
		int middleindex = (left + right) / 2;
		T middleValue = vec[middleindex];
		if (middleValue < target) {
			left = middleindex + 1;
		}
		else if (middleValue > target) {
			right = middleindex - 1;
		}
		else {
			return true;
		}
	}
	return false;
}
```

## 查找是否有相同的值

```cpp
/// <summary>
/// find if vector has equal value item
/// </summary>
/// <typeparam name="T">typename</typeparam>
/// <param name="vec"></param>
/// <returns></returns>
bool findEqual(vector<T> vec) {
	map<T, bool>hash;
	for (int i = 0; i < vec.size(); i++) {
		if (hash.find(vec[i]) == hash.end()) {
			hash[vec[i]] = true;
		}
		else {
			return true;
		}
	}
	return false;
}

```

# 拆分字符串

## 生成单词

```cpp
/// <summary>
/// detached string
/// </summary>
/// <param name="str">object string</param>
/// <returns>vector of the string</returns>
vector<string> detachedString(string& str) {
	istringstream ss(str);
	vector<string>res;
	string temp;
	while (ss >> temp) {
		res.push_back(temp);
	}
	return res;
}
// another edition
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

int main () {
	std::vector<std::string> coll;

	// read all words from the standard input
	std::copy ( std::istream_iterator<std::string> ( std::cin ) , std::istream_iterator<std::string> () , std::back_inserter ( coll ) );

	// sort elements
	sort ( coll.begin () , coll.end () );

	// print all elements without duplicates
	std::unique_copy ( coll.begin () , coll.end () , std::ostream_iterator<std::string> ( std::cout , "\n" ) );

	//exit
	std::exit ( EXIT_SUCCESS );
}
```

# 计数

## map

```cpp
/// <summary>
/// count for the value
/// </summary>
/// <typeparam name="T">typename</typeparam>
/// <param name="vec">vector</param>
/// <returns>return map</returns>
template<typename T>
map<T, int> count(vector<T>& vec) {
	map<T, int>res;
	for (int i = 0; i < vec.size(); i++) {
		if (res.find(vec[i]) == res.end()) {
			res[vec[i]] = 1;
		}
		else {
			res[vec[i]]++;
		}
	}
	return res;
}
```

## vector+pair

```cpp
/// <summary>
/// count number of the vector item value
/// </summary>
/// <typeparam name="T">typename</typeparam>
/// <param name="vec">vector</param>
/// <returns>return pair of the vector</returns>
template<typename T>
vector<pair<T, int>> count(vector<T>& vec) {
	vector<pair<T, int>>res;
	if (vec.size() == 0) {
		return res;
	}
	else {
		pair<T, int>temp;
		temp.first = vec[0];
		temp.second = 1;
		res.push_back(temp);
		for (int i = 1; i < vec.size(); i++) {
			bool find = false;
			for (int j = 0; j < res.size(); j++) {
				if (res[j].first == vec[i]) {
					res[j].second++;
					find = true;
					break;
				}
			}
			if (!find) {
				temp.first = vec[i];
				temp.second = 1;
				res.push_back(temp);
			}
		}
		return res;
	}
}
```

## vector(26,0)——只出现英文单词

```cpp
string str = "frtrhehgvaewhrqhfbvzvjkaheglaefsdarg";
vector<int>count(26, 0);
for (char x : str) {
	count[x - 'a']++;
}
for (int i = 0; i < count.size(); i++) {
	if (count[i] != 0) {
		cout << setw(4) << left << char(i + 'a') << count[i] << endl;
	}
}
```



# 质数

```cpp
/// <summary>
/// get primes
/// </summary>
/// <param name="n">range of the primes</param>
/// <returns>vector of the primes</returns>
vector<int> primes(int n) {
	vector<int>res;
	if (n <= 0) {
		return res;
	}
	bool* notPrime = new bool[n];
	for (int i = 0; i < n; i++) {
		notPrime[i] = false;
	}
	for (int i = 2; i < n; i++) {
		if (notPrime[i] == false) {
			res.push_back(i);
		}
		for (int j = 2; i * j < n; j++) {
			notPrime[i * j] = true;
		}
	}
	return res;
}
```

# 最小公约数

```cpp
//辗转相除法求最大公约数函数
int divisor(int a, int b) {
	int temp;

	//比较两个数的大小，值大的数为a，值小的数为b
	if (a < b) {
		temp = a;
		a = b;
		b = temp;
	}

	//求余
	while (b != 0) {
		temp = a % b;
		a = b;
		b = temp;
	}
	return a;
}

//求最小公倍数
int multiple(int a, int b) {
	int divisor(int a, int b);
	int temp;
	temp = divisor(a, b);
	return(a * b / temp);
}

//函数递归调用求最大公约数
int gcd(int a, int b) {
	if (a % b == 0) {
		return b;
	}
	else {
		return gcd(b, a % b);
	}
}

//穷举法求最大公约数
int divisor1(int a, int b) {
	int temp;
	temp = (a > b) ? b : a;   //求较小值
	while (temp > 0) {
		if (a % temp == 0 && b % temp == 0) {
			break;
		}
		else {
			temp--;
		}
	}
	return (temp);
}

//穷举法求最小公倍数
int multiple1(int a, int b) {
	int p, q, temp;
	p = (a > b) ? a : b;  //求两数中的最大值
	q = (a > b) ? b : a;  //求两数中的最小值
	temp = p;
	while (1) {
		if (p % q == 0) {
			break;
		}
		else {
			p += temp;
		}
	}
	return (p);
}

//更相减损法求最大公约数
int gcd1(int a, int b) {
	int i = 0, temp, x = 0;
	while (a % 2 == 0 && b % 2 == 0) {    //m,n有公约数2时
		a /= 2;
		b /= 2;
		i += 1;
	}
	//a,b的值互换
	if (a < b) {
		temp = a;
		a = b;
		b = temp;
	}
	while (x) {
		x = a - b;
		a = (b > x) ? b : x;   
		b = (b < x) ? b : x;
		if (b == (a - b)) {    //差和减数相等
			break;
		}
	}
	if (i == 0) {
		return b;
	}
	else {
		return (int)pow(2, i)*b;
	}
}
```

# 最大公倍数

```cpp
int lcm(int m, int n)
{
	int max;
	if (m < n)
	{
		max = n;
	}
	else
	{
		max = m;
	}
	
	while (true)
	{
		if (max % m == 0 && max % n == 0 )
		{
			return max;
		}
		
		max++;
	}
}
```

# 进制转换

## 十进制转二进制

```cpp
/// <summary>
/// get Binary
/// </summary>
/// <param name="x">Decimalism value</param>
/// <returns>vector of the Binary Code</returns>
vector<int> getBinary(int x){
    vector<int>res(32,0);
    if(x>=0){
        int i=0;
        while(x!=0){
            res[31-i]=x%2;
            x/=2;
            i++;
        }
    }
    else{
        x=abs(x);
        int i=0;
        while(x!=0){
            res[31-i]=x%2;
            x/=2;
            i++;
        }
        for(int i=0;i<32;i++){
            if(res[i]==0){
                res[i]=1;
            }
            else{
                res[i]=0;
            }
        }
        for(int i=31;i>=0;i--){
            if(res[i]==0){
                res[i]=1;
                break;
            }
            else{
                res[i]=0;
            }
        }
    }
    return res;
}
```

## 十进制转十六进制

```cpp
/// <summary>
/// get Hex
/// </summary>
/// <param name="x">Hex value</param>
/// <returns>vector of the Hex Code</returns>
string toHex(int num) {
    if(num==0){
        return "0";
    }
    int len=0;
    string ans="";
    while(num&&len<8){
        int bit=num&15;
        if(bit<10){
            ans=(char)('0'+bit)+ans;
        }
        else{
            ans=(char)('a'+bit-10)+ans;
        }
        num>>=4;
        len++;
    }
    return ans;
}
```

# 补数

```cpp
int findComplement(int num) {
    vector<int>res;
    while(num!=0){
        res.push_back(num%2);
        num/=2;
    }
    for(int &x:res){
        if(x==1){
            x=0;
        }
        else{
            x=1;
        }
    }
    int count=0;
    for(int i=0;i<res.size();i++){
        count+=pow(2,i)*res[i];
    }
    return count;
}
```

# 判断是非为n的幂

```cpp
bool isPowerOfN(int num,int n) {
	if (num <= 0) {
		return false;
	}
	while (num != 0) {
		if (num % n != 0 and num != 1) {
			return false;
		}
		else {
			num /= n;
		}
	}
	return true;
}
```

# 获得不同的vector序列	unique

```cpp
/// <summary>
/// greater to lower
/// </summary>
/// <typeparam name="T">typename</typeparam>
/// <param name="a"></param>
/// <param name="b"></param>
/// <returns>
/// true: don't swap
/// false: swap
/// </returns>
template<typename T>
bool cmp(T a, T b) {
	if (a > b) {
		return true;
	}
	else {
		return false;
	}
}
/// <summary>
/// get difference vector
/// </summary>
/// <typeparam name="T">typename</typeparam>
/// <param name="vec">vector</param>
/// <returns>difference vector</returns>
template<typename T>
vector<T> getDifference(vector<T> vec) {
	vector<T>res = vec;
	sort(res.begin(), res.end(), cmp<T>);
	auto iter = unique(res.begin(), res.end());
	res.erase(iter, res.end());
	return res;
}
```

# DP动态规划

```cpp
int longestIncreasingSubsequence(vector<int>& nums) {
    if (nums.size() == 0) {
        return 0;
    }
    int res = 1;
    vector<int> LIS(nums.size(), 1);
    for (int i = 1; i < nums.size(); ++i) {
        for (int j = 0; j < i; ++j) {
            if (nums[i] > nums[j]) {
                LIS[i] = max(LIS[i], LIS[j] + 1);
            }
        }
        res = max(res, LIS[i]);
    }
    return res;
}
int jump(vector<int> &A) {
    int n=A.size();
    vector<int>dp(n);
    dp[0]=0;
    for(int i=1;i<n;i++){
        dp[i]=INT_MAX;
        for(int j=0;j<i;j++){
            if(A[j]+j>=i){
                dp[i]=min(dp[i],dp[j]+1);
            }
        }
    }
    return dp[n-1];
}
```

>    ### *重要三要素：*
>
>    ####      (1) 每个问题的阶段.
>
>    ####     (2) 每个阶段的状态.
>
>    ####     (3) 上一阶段状态转换到下一阶段状态之间的递推关系.
>
>    ####     递推关系必须是从次小的问题开始到较大的问题之间的转化, 从这个角度来说 , DP算法往往可以用递归程序来实现 ,  不过因为递推可以充分利用前面保存的子问题的解来减少重复计算 ,  所以对于大规模问题来说 ,  有递归不可比拟的优势 ,  这也是DP算法的核心之处。确定了动态规划的这三要素之后呢 ,  整个求解过程就可以用一个最优决策表来描述 ,  最优决策表是一个二维表 ,  其中行表示决策的阶段 ,  列表示问题状态，表格需要填写的数据一般对应此问题的在某个阶段某个状态下的最优值（如最短路径问题,  最长公共子序列问题 ,  最大价值问题等） ,  填表的过程就是根据递推关系 ,  从 1 行 1 列开始 ,  以行或者列优先的顺序 ,  依次填写表格，最后根据整个表格的数据通过简单的取舍或者运算求得问题的最优解：f(i, j) = max {f(i - 1, j), f(i - 1, j - dp[n]) + base(i, j)}。

---

# DFS

深度优先遍历图算法步骤：

1.   访问顶点v；
2.   依次从v的未被访问的邻接点出发，对图进行深度优先遍历；直至图中和v有路径相通的顶点都被访问；
3.   若此时图中尚有顶点未被访问，则从一个未被访问的顶点出发，重新进行深度优先遍历，直到图中所有顶点均被访问过为止。

# LeetCode

# 1. A + B 问题

给出两个整数 a*a* 和 b*b* , 求他们的和。

### 样例

**样例 1:**

```
输入:  a = 1, b = 2
输出: 3	
样例解释: 返回a+b的结果.
```

**样例 2:**

```
输入:  a = -1, b = 1
输出: 0	
样例解释: 返回a+b的结果.
```

### 挑战

显然你可以直接 return a + b，但是你是否可以挑战一下不这样做？（不使用++等算数运算符）

### 说明

a和b都是 `32位` 整数么？

-    是的

我可以使用位运算符么？

-    当然可以

### 注意事项

你不需要从输入流读入数据，只需要根据`aplusb`的两个参数a和b，计算他们的和并返回就行。

```cpp
class Solution {
public:
    /**
     * @param a: An integer
     * @param b: An integer
     * @return: The sum of a and b 
     */
    int aplusb(int a, int b) {
        return a+b;
    }
};
```

# 2. 尾部的零

设计一个算法，计算出n阶乘中尾部零的个数

### 样例

```
样例  1:
	输入: 11
	输出: 2
	
	样例解释: 
	11! = 39916800, 结尾的0有2个。

样例 2:
	输入:  5
	输出: 1
	
	样例解释: 
	5! = 120， 结尾的0有1个。
```

### 挑战

O(logN)的时间复杂度

```cpp
class Solution {
public:
    /*
     * @param n: A long integer
     * @return: An integer, denote the number of trailing zeros in n!
     */
    long long trailingZeros(long long n) {
        long long sum = 0;
		while (n != 0) {
			sum += n / 5;
			n /= 5;
		}
		return sum;
    }
};
```

# 3. 统计数字

计算数字 k 在 0 到 n 中的出现的次数，k 可能是 0~9 的一个值。

### 样例

**样例 1：**

```
输入：
k = 1, n = 1
输出：
1
解释：
在 [0, 1] 中，我们发现 1 出现了 1 次 (1)。
```

**样例 2：**

```
输入：
k = 1, n = 12
输出：
5
解释：
在 [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12] 中，我们发现 1 出现了 5 次 (1, 10, 11, 12)(注意11中有两个1)。
```

```cpp
class Solution {
public:
    /**
     * @param k: An integer
     * @param n: An integer
     * @return: An integer denote the count of digit k in 1..n
     */
    int digitCounts(int k, int n) {
        int count = 0;
		if (k == 0) {
			count = 1;
		}
		for (int i = 1; i <= n; i++) {
			int number = i;
			while (number > 0) {
				if (number % 10 == k) {
					count++;
				}
				number /= 10;
			}
		}
		return count;
    }
};
```

# 4. 丑数 II

设计一个算法，找出只含素因子`2`，`3`，`5` 的第 *n* 小的数。

符合条件的数如：`1, 2, 3, 4, 5, 6, 8, 9, 10, 12...`

### 样例

**样例 1：**

```
输入：9
输出：10
```

**样例 2：**

```
输入：1
输出：1
```

### 挑战

要求时间复杂度为 O(*n*log*n*) 或者 O(*n*)。

### 注意事项

我们可以认为 `1` 也是一个丑数。

```cpp
class Solution {
public:
    /**
     * @param n: An integer
     * @return: return a  integer as description.
     */
    int nthUglyNumber(int n) {
		int* uglys = new int[n];
		uglys[0] = 1;
		int next = 1;
		int* p2 = uglys;
		int* p3 = uglys;
		int* p5 = uglys;
		while (next < n) {
			int m = min(min(*p2 * 2, *p3 * 3), *p5 * 5);
			uglys[next] = m;
			while (*p2 * 2 <= uglys[next]) {
				*p2++;
			}
			while (*p3 * 3 <= uglys[next]) {
				*p3++;
			}
			while (*p5 * 5 <= uglys[next]) {
				*p5++;
			}
			next++;
		}
		int uglyNum = uglys[n - 1];
		delete[]uglys;
		return uglyNum;
    }
};
```

# 5. 第k大元素

在数组中找到第 k 大的元素。

### 样例

**样例 1：**

```
输入：
n = 1, nums = [1,3,4,2]
输出：
4
```

**样例 2：**

```
输入：
n = 3, nums = [9,3,2,4,8]
输出：
4
```

### 挑战

要求时间复杂度为O(n)，空间复杂度为O(1)。

### 注意事项

你可以交换数组中的元素的位置

```cpp
class Solution {
public:
    /**
     * @param n: An integer
     * @param nums: An array
     * @return: the Kth largest element
     */
	int kthLargestElement(int k, vector<int>& nums) {
		int n = nums.size();
		k = n - k;
		return partition(nums, 0, n - 1, k);
	}
	int partition(vector<int>& nums, int start, int end, int k) {
		int left = start, right = end;
		int pivot = nums[left];
		while (left <= right) {
			while (left <= right and nums[left] < pivot) {
				left++;
			}
			while (left <= right and nums[right] > pivot) {
				right--;
			}
			if (left <= right) {
				swap(nums[left], nums[right]);
				left++;
				right--;
			}
		}
		if (k <= right) {
			return partition(nums, start, right, k);
		}
		if (k >= left) {
			return partition(nums, left, end, k);
		}
		return nums[k];
	}
};
```

# 6. 合并排序数组

合并两个有序升序的整数数组A和B变成一个新的数组。新数组也要有序。

### 样例

**样例 1:**

```
输入: A=[1], B=[1]
输出:[1,1]	
样例解释: 返回合并后的数组。
```

**样例 2:**

```
输入: A=[1,2,3,4], B=[2,4,5,6]
输出: [1,2,2,3,4,4,5,6]	
样例解释: 返回合并后的数组。
```

### 挑战

你能否优化你的算法，如果其中一个数组很大而另一个数组很小？

```cpp
class Solution {
public:
    /**
     * @param A: sorted integer array A
     * @param B: sorted integer array B
     * @return: A new sorted integer array
     */
    vector<int> mergeSortedArray(vector<int> &A, vector<int> &B) {
		if (A.size() > B.size()) {
			return insertSort(A, B);
		}
		else {
			return insertSort(B, A);
		}
	}

	vector<int> insertSort(vector<int>& C, vector<int>& D) {
		int length = C.size() + D.size(), size = C.size();
		int j = 0;
		C.insert(C.end(), D.begin(), D.end());
		for (int i = size; i < length; i++) {
			int temp = C[i];
			for (j = i - 1; j >= 0 && temp < C[j]; j--) {
				C[j + 1] = C[j];
			}
			C[j + 1] = temp;
		}
		for (int x : C) {
			cout << x << " ";
		}
		return C;
	}
};
```

# 8. 旋转字符串

给定一个字符串（以字符数组的形式给出）和一个偏移量，根据偏移量`原地`旋转字符串(从左向右旋转)。

### 样例

**样例 1:**

```
输入:  str="abcdefg", offset = 3
输出:  str = "efgabcd"	
样例解释:  注意是原地旋转，即str旋转后为"efgabcd"
```

**样例 2:**

```
输入: str="abcdefg", offset = 0
输出: str = "abcdefg"	
样例解释: 注意是原地旋转，即str旋转后为"abcdefg"
```

**样例 3:**

```
输入: str="abcdefg", offset = 1
输出: str = "gabcdef"	
样例解释: 注意是原地旋转，即str旋转后为"gabcdef"
```

**样例 4:**

```
输入: str="abcdefg", offset =2
输出: str = "fgabcde"	
样例解释: 注意是原地旋转，即str旋转后为"fgabcde"
```

**样例 5:**

```
输入: str="abcdefg", offset = 10
输出: str = "efgabcd"	
样例解释: 注意是原地旋转，即str旋转后为"efgabcd"
```

### 挑战

在数组上原地旋转，使用O(1)的额外空间

### 说明

`原地旋转`意味着你要在s本身进行修改。你不需要返回任何东西。

### 注意事项

offset >= 0
str的长度 >= 0

```cpp
class Solution {
public:
    /**
     * @param str: An array of char
     * @param offset: An integer
     * @return: nothing
     */
    void rotateString(string &str, int offset) {
		if (str.size() == 0) {
			return;
		}
		offset %= str.size();
		string tempA = str.substr(0, str.size() - offset);
		string tempB = str.substr(str.size() - offset, str.size());
		str = tempB + tempA;
	}
};
```

# 9. Fizz Buzz 问题

给你一个整数*n*. 从 *1* 到 *n* 按照下面的规则打印每个数：

-    如果这个数被3整除，打印`fizz`.
-    如果这个数被5整除，打印`buzz`.
-    如果这个数能同时被`3`和`5`整除，打印`fizz buzz`.
-    如果这个数既不能被 `3` 整除也不能被 `5` 整除，打印数字`本身。`

### 样例

比如 *n* = `15`, 返回一个字符串数组：

```
[
  "1", "2", "fizz",
  "4", "buzz", "fizz",
  "7", "8", "fizz",
  "buzz", "11", "fizz",
  "13", "14", "fizz buzz"
]
```

### 挑战

你是否可以只用一个 `if` 来实现

```cpp
class Solution {
public:
    /**
     * @param n: An integer
     * @return: A list of strings.
     */
    vector<string> fizzBuzz(int n) {
		vector<string> result(n);
		for (int i = 1; i <= n; i++) {
			if (i % 15 == 0) {
				result[i - 1] = "fizz buzz";
			}
			else if (i % 3 == 0) {
				result[i - 1] = "fizz";
			}
			else if (i % 5 == 0) {
				result[i - 1] = "buzz";
			}
			else {
				result[i - 1] = to_string(i);
			}
		}
		return result;
	}
};
```

# 12. 带最小值操作的栈

实现一个栈, 支持以下操作:

-    `push(val)` 将 val 压入栈
-    `pop()` 将栈顶元素弹出, 并返回这个弹出的元素
-    `min()` 返回栈中元素的最小值

要求 O(1) 开销.

### 样例

**样例 2:**

```
输入: 
  push(1)
  min()
  push(2)
  min()
  push(3)
  min()
输出: 
  1
  1
  1
```

### 注意事项

保证栈中没有数字时不会调用 `min()`

```cpp
class MinStack {
public:
    stack<int> s1;
    stack<int> s2;
    MinStack() {
        // do intialization if necessary
    }

    /*
     * @param number: An integer
     * @return: nothing
     */
    void push(int number) {
        // write your code here
        s1.push(number);
        if(!s2.empty()){
            int temp=s2.top();
            if(number<temp){
                s2.push(number);
            }else{
                s2.push(temp);
            }
        }
        else{
            s2.push(number);
        }
    }

    /*
     * @return: An integer
     */
    int pop() {
        // write your code here
        int temp=s1.top();
        s1.pop();
        s2.pop();
        return temp;
    }

    /*
     * @return: An integer
     */
    int min() {
        // write your code here
        return s2.top();
    }
};
```

# 13. 字符串查找

对于一个给定的 source 字符串和一个 target 字符串，你应该在 source 字符串中找出 target 字符串出现的第一个位置(从0开始)。如果不存在，则返回 `-1`。

### 样例

**样例 1:**

```
输入: source = "source" ， target = "target"
输出:-1	
样例解释: 如果source里没有包含target的内容，返回-1
```

**样例 2:**

```
输入: source = "abcdabcdefg" ，target = "bcd"
输出: 1	
样例解释: 如果source里包含target的内容，返回target在source里第一次出现的位置
```

### 挑战

O(n2)的算法是可以接受的。如果你能用O(n)的算法做出来那更加好。（提示：KMP）

### 说明

在面试中我是否需要实现KMP算法？

-    不需要，当这种问题出现在面试中时，面试官很可能只是想要测试一下你的基础应用能力。当然你需要先跟面试官确认清楚要怎么实现这个题。

```cpp
class Solution {
public:
    /**
     * @param source: 
     * @param target: 
     * @return: return the index
     */
    int strStr(string &source, string &target) {
		return source.find(target);
    }
};
```

# 14. 二分查找

给定一个排序的整数数组（升序）和一个要查找的整数`target`，用`O(logn)`的时间查找到target第一次出现的下标（从0开始），如果target不存在于数组中，返回`-1`。

### 样例

```
样例  1:
	输入:[1,4,4,5,7,7,8,9,9,10]，1
	输出: 0
	
	样例解释: 
	第一次出现在第0个位置。

样例 2:
	输入: [1, 2, 3, 3, 4, 5, 10]，3
	输出: 2
	
	样例解释: 
	第一次出现在第2个位置
	
样例 3:
	输入: [1, 2, 3, 3, 4, 5, 10]，6
	输出: -1
	
	样例解释: 
	没有出现过6， 返回-1
```

### 挑战

如果数组中的整数个数超过了2^32，你的算法是否会出错？

```cpp
class Solution {
public:
    /**
     * @param nums: The integer array.
     * @param target: Target to find.
     * @return: The first position of target. Position starts from 0.
     */
    int binarySearch(vector<int> &nums, int target) {
		int tempa = 0, tempb = nums.size();
		while (tempb >= tempa) {
			int medium = (tempa + tempb) / 2;
			if (nums[medium] > target) {
				tempb = medium-1;
			}
			else if (nums[medium] == target) {
				while (nums[medium] == nums[medium - 1]) {
					medium--;
				}
				return medium;
			}
			else {
				tempa = medium+1;
			}
		}
		return -1;
	}
};
```

# 15. 全排列

给定一个数字列表，返回其所有可能的排列。

### 样例

**样例 1：**

```
输入：[1]
输出：
[
  [1]
]
```

**样例 2：**

```
输入：[1,2,3]
输出：
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

### 挑战

使用递归和非递归分别解决。

### 注意事项

你可以假设没有重复数字。

```cpp
class Solution {
public:
	/*
	 * @param nums: A list of integers.
	 * @return: A list of permutations.
	 */
	vector<vector<int>> permute(vector<int>& nums) {
		vector<vector<int>>results;
		if (nums.size() == 0) {
			results.push_back(vector<int>());
			return results;
		}
		vector<bool>used(nums.size(), 0);
		vector<int>current;
		dfs(nums, used, current, results);
		return results;
	}
	void dfs(vector<int>nums, vector<bool>& used, vector<int>& current, vector<vector<int>>& results) {
		if (current.size() == nums.size()) {
			results.push_back(current);
			return;
		}
		for (int i = 0; i < nums.size(); i++) {
			if (used[i]) {
				continue;
			}
			current.push_back(nums[i]);
			used[i] = true;
			dfs(nums, used, current, results);
			used[i] = false;
			current.pop_back();
		}
		return;
	}
};
```

# 16. 带重复元素的排列

给出一个具有重复数字的列表，找出列表所有**不同**的排列。

### 样例

**样例 1：**

```
输入：[1,1]
输出：
[
  [1,1]
]
```

**样例 2：**

```
输入：[1,2,2]
输出：
[
  [1,2,2],
  [2,1,2],
  [2,2,1]
]
```

### 挑战

使用递归和非递归分别完成该题。

```cpp
class Solution {
private:
	void helper(vector<vector<int>>& results, vector<int>& permutation, vector<int>& nums, bool used[]) {
		if (nums.size() == permutation.size()) {
			results.push_back(permutation);
			return;
		}
		for (int i = 0; i < nums.size(); i++) {
			if (used[i]) {
				continue;
			}
			if (i > 0 && used[i - 1] == false && nums[i] == nums[i - 1]) {
				continue;
			}
			used[i] = true;
			permutation.push_back(nums[i]);
			helper(results, permutation, nums, used);
			permutation.pop_back();
			used[i] = false;
		}
	}
public:
	/*
	 * @param nums: A list of integers.
	 * @return: A list of permutations.
	 */
	vector<vector<int>> permuteUnique(vector<int>& nums) {
		vector<vector<int>>results;
		vector<int>permutation;
		bool* used = new bool[nums.size()];
		for (int i = 0; i < nums.size(); i++) {
			used[i] = false;
		}
		sort(nums.begin(), nums.end());
		helper(results, permutation, nums, used);
		return results;
	}
};
```

# 17. 子集

给定一个含不同整数的集合，返回其所有的子集。

### 样例

**样例 1：**

```
输入：[0]
输出：
[
  [],
  [0]
]
```

**样例 2：**

```
输入：[1,2,3]
输出：
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

### 挑战

你可以同时用递归与非递归的方式解决么？

### 注意事项

子集中的元素排列必须是非降序的，解集必须不包含重复的子集。

```cpp
class Solution {
public:
	/**
	 * @param nums: A set of numbers
	 * @return: A list of lists
	 */
	vector<vector<int>> subsets(vector<int>& nums) {
		vector<vector<int>>results;
		vector<int> subset;
		sort(nums.begin(), nums.end());
		helper(results, subset, nums, 0);
		return results;
	}
private:
	void helper(vector<vector<int>>& results, vector<int>& subset, vector<int>& nums, int start) {
		results.push_back(subset);
		for (int i = start; i < nums.size(); i++) {
			subset.push_back(nums[i]);
			helper(results, subset, nums, i + 1);
			subset.pop_back();
		}
	}
};
```

# 20. 骰子求和

扔 *n* 个骰子，向上面的数字之和为 *S*。给定 *n*，请列出所有可能的 *S* 值及其相应的概率。

### 样例

**样例 1：**

```
输入：n = 1
输出：[[1, 0.17], [2, 0.17], [3, 0.17], [4, 0.17], [5, 0.17], [6, 0.17]]
解释：掷一次骰子，向上的数字和可能为1,2,3,4,5,6，出现的概率均为 0.17。
```

**样例 2：**

```
输入：n = 2
输出：[[2,0.03],[3,0.06],[4,0.08],[5,0.11],[6,0.14],[7,0.17],[8,0.14],[9,0.11],[10,0.08],[11,0.06],[12,0.03]]
解释：掷两次骰子，向上的数字和可能在[2,12]，出现的概率是不同的。
```

### 注意事项

你不需要关心结果的准确性，我们会帮你输出结果。

```cpp
class Solution {
public:
    /**
     * @param n an integer
     * @return a list of pair<sum, probability>
     */
    vector<pair<int, double>> dicesSum(int n) {
		vector<map<int, double>>dp(n + 1);
		dp[1] = { {1,1 / 6.0},{2,1 / 6.0},{3,1 / 6.0},{4,1 / 6.0},{5,1 / 6.0},{6,1 / 6.0} };
		for (int i = 2; i <= n; i++) {
			for (auto a1 : dp[i - 1]) {
				for (auto a2 : dp[1]) {
					dp[i][a1.first + a2.first] += a1.second * a2.second;
				}
			}
		}
		vector<pair<int, double>>res;
		for (auto a : dp[n]) {
			res.push_back({ a.first,a.second });
		}
		return res;
    }
};
```

# 21. 移动的圆

题目将给出两个圆A和B的圆心坐标(x,y)和半径r，现给你一个点P,使圆A圆心沿直线运动至点P。
请问圆A在运动过程中是否会与圆B相交？（运动过程包括起点和终点）
若会相交返回1，否则返回-1。

### 样例

**样例 1**

```
输入：[0,0,2.5,3,2,0.5,0,2]
输出：1
样例解释：圆A的圆心（0，0），半径为2.5，圆B的圆心（3，2），半径为0.5，点P（0，2）
```

**样例 2**

```
输入：[0,0,2,5,0,1,0,2]
输出：-1
样例解释：圆A的圆心（0，0），半径为2，圆B的圆心（5，0），半径为1，点P（0，2）
```

### 注意事项

两个圆的半径均不超过10000。
横纵坐标值的绝对值均不超过10000。
输入数组的意义为[X_A*X*​*A*​​,Y_A*Y*​*A*​​,R_A*R*​*A*​​,X_B*X*​*B*​​,Y_B*Y*​*B*​​,R_B*R*​*B*​​,X_P*X*​*P*​​,Y_P*Y*​*P*​​]。

```cpp
class Solution {
public:
	/**
	 * @param position: the position of circle A,B and point P.
	 * @return: if two circle intersect return 1, otherwise -1.
	 */
	typedef struct point {
		double x, y;
	}point;
	double xmult(point B, point C, point A) {
		return (B.x - A.x) * (C.y - A.y) - (C.x - A.x) * (B.y - A.y);
	}
	double distance(point A, point B) {
		return sqrt((A.x - B.x) * (A.x - B.x) + (A.y - B.y) * (A.y - B.y));
	}
	double dis_ptoline(point A, point B, point C) {
		return fabs(xmult(A, B, C)) / distance(B, C);
	}
	int IfIntersect(vector<double>& position) {
		point A, B, P, M;
		double ra, rb;
		double dmin, dmax;
		A.x = position[0];//initialize
		A.y = position[1];
		ra = position[2];
		B.x = position[3];
		B.y = position[4];
		rb = position[5];
		P.x = position[6];
		P.y = position[7];
		M.x = B.x - (P.y - A.y), M.y = B.y + (P.x - A.x);
		if (xmult(A, B, M) * xmult(B, P, M) >= 0) {
			if (A.x == P.x && A.y == P.y) {
				dmin = distance(B, A);
			}
			else {
				dmin = dis_ptoline(B, A, P);
			}
		}
		else {
			dmin = min(distance(A, B), distance(P, B));
		}
		dmax = max(distance(A, B), distance(P, B));
		if (dmin > ra + rb || dmax < fabs(ra - rb)) {
			return -1;
		}
		return 1;
	}
};
```

# 22. 列表扁平化

给定一个列表，该列表中的每个元素要么是个列表，要么是整数。将其变成一个只包含整数的简单列表。

### 样例

```
样例  1:
	输入: [[1,1],2,[1,1]]
	输出:[1,1,2,1,1] 
	
	样例解释:
	将其变成一个只包含整数的简单列表。


样例 2:
	输入: [1,2,[1,2]]
	输出:[1,2,1,2]
	
	样例解释: 
	将其变成一个只包含整数的简单列表。
	
样例 3:
	输入:[4,[3,[2,[1]]]]
	输出:[4,3,2,1]
	
	样例解释: 
	将其变成一个只包含整数的简单列表。
	
```

### 挑战

请用非递归方法尝试解答这道题。

### 注意事项

如果给定的列表中的要素本身也是一个列表，那么它也可以包含列表。

```cpp
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * class NestedInteger {
 *   public:
 *     // Return true if this NestedInteger holds a single integer,
 *     // rather than a nested list.
 *     bool isInteger() const;
 *
 *     // Return the single integer that this NestedInteger holds,
 *     // if it holds a single integer
 *     // The result is undefined if this NestedInteger holds a nested list
 *     int getInteger() const;
 *
 *     // Return the nested list that this NestedInteger holds,
 *     // if it holds a nested list
 *     // The result is undefined if this NestedInteger holds a single integer
 *     const vector<NestedInteger> &getList() const;
 * };
 */
class Solution {
public:
    // @param nestedList a list of NestedInteger
    // @return a list of integer
    vector<int> flatten(vector<NestedInteger> &nestedList) {
        vector<int>res;
        flatten(nestedList,res);
        return res;
    }
    void flatten(const vector<NestedInteger> &nestedList,vector<int>&result){
        for(auto ni:nestedList){
            if(ni.isInteger()){
                result.push_back(ni.getInteger());
            }else{
                flatten(ni.getList(),result);
            }
        }
    }
};
```

# 23. 判断数字与字母字符

给出一个字符`c`，你需要判断它是不是一个数字字符或者字母字符。
如果是，返回`true`，如果不是返回`false`。

### 样例

**样例 1:**

```plain
输入：'1'
输出：true
```

### 注意事项

如果您使用的是Python语言，那么输入将是一个长度为1的字符串。

```cpp
class Solution {
public:
    /**
     * @param c: A character.
     * @return: The character is alphanumeric or not.
     */
	bool isAlphanumeric(char c) {
		if (isalpha(c) || isdigit(c)) {
			return true;
		}
		else {
			return false;
		}
	}
};
```

# 25. 打印X

输入一个正整数N， 你需要按如下方式返回一个字符串列表。

### 样例

**样例 1:**

```
输入：1
输出：
[
"X"
]
```

**样例 2:**

```
输入：2
输出：
[
"XX",
"XX"
]
```

**样例 3:**

```
输入：3
输出：
[
"X X",
" X ",
"X X"
]
```

**样例 4:**

```
输入：4
输出：
[
"X  X",
" XX ",
" XX ",
"X  X"
]
```

**样例 5:**

```
输入：5
输出：
[
"X   X",
" X X ",
"  X  ",
" X X ",
"X   X"
]
```

输入测试数据（每行一个参数）如何理解测试数据？

```cpp
class Solution {
public:
    /**
     * @param n: An integer.
     * @return: A string list.
     */
	vector<string> printX(int n) {
		vector<string>result;
		for (int i = 0; i < n; i++) {
			string temp(n, ' ');
			temp[i] = 'X';
			temp[n - i - 1] = 'X';
			result.push_back(temp);
		}
		return result;
	}
};
```

# 28. 搜索二维矩阵

写出一个高效的算法来搜索 *m* × *n*矩阵中的值。

这个矩阵具有以下特性：

-    每行中的整数从左到右是排序的。
-    每行的第一个数大于上一行的最后一个整数。

### 样例

```
样例  1:
	输入: [[5]],2
	输出: false
	
	样例解释: 
  没有包含，返回false。

样例 2:
	输入:  
[
  [1, 3, 5, 7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
],3
	输出: true
	
	样例解释: 
	包含则返回true。
```

### 挑战

O(log(n) + log(m)) 时间复杂度

```cpp
class Solution {
public:
    /**
     * @param matrix: matrix, a list of lists of integers
     * @param target: An integer
     * @return: a boolean, indicate whether matrix contains target
     */
    bool searchMatrix(vector<vector<int>> &matrix, int target) {
		int n = matrix.size();
		if (n == 0) {
			return false;
		}
		int m = matrix[0].size();
		if (m == 0) {
			return false;
		}
		int start = 0, end = n * m - 1;
		while (start + 1 < end) {
			int mid = start + (end - start) / 2;
			int row = mid / m;
			int col = mid % m;
			if (matrix[row][col] < target) {
				start = mid;
			}
			else {
				end = mid;
			}
		}
		if (matrix[start / m][start % m] == target) {
			return true;
		}
		if (matrix[end / m][end % m] == target) {
			return true;
		}
		return false;
    }
};
```

# 35. 翻转链表

翻转一个链表

### 样例

**样例 1:**

```
输入: 1->2->3->null
输出: 3->2->1->null
```

**样例 2:**

```
输入: 1->2->3->4->null
输出: 4->3->2->1->null
```

### 挑战

在原地一次翻转完成.

```cpp
/**
 * Definition of singly-linked-list:
 * class ListNode {
 * public:
 *     int val;
 *     ListNode *next;
 *     ListNode(int val) {
 *        this->val = val;
 *        this->next = NULL;
 *     }
 * }
 */

class Solution {
public:
    /**
     * @param head: n
     * @return: The new head of reversed linked list.
     */
    ListNode * reverse(ListNode * head) {
		ListNode* result = nullptr;
		while (head != nullptr) {
			ListNode* temp = head->next;
			head->next = result;
			result = head;
			head = temp;
		}
		return result;
    }
};
```

# 37. 反转一个3位整数

反转一个只有3位数的整数。

### 样例

**样例 1:**

```
输入: number = 123
输出: 321
```

**样例 2:**

```
输入: number = 900
输出: 9
```

### 注意事项

你可以假设输入一定是一个只有三位数的整数，这个整数大于等于100，小于1000。

```cpp
class Solution {
public:
    /**
     * @param number: A 3-digit number.
     * @return: Reversed number.
     */
    int reverseInteger(int number) {
		return number / 100 + ((number / 10) % 10) * 10 + (number % 10) * 100;
    }
};
```

# 39. 恢复旋转排序数组

给定一个**旋转**排序数组，在原地恢复其排序。（升序）

### 样例

**样例1:**
`[4, 5, 1, 2, 3]` -> `[1, 2, 3, 4, 5]`
**样例2:**
`[6,8,9,1,2]` -> `[1,2,6,8,9]`

### 挑战

使用O(1)的额外空间和O(*n*)时间复杂度

### 说明

什么是旋转数组？

-    比如，原始数组为[1,2,3,4], 则其旋转数组可以是[1,2,3,4], [2,3,4,1], [3,4,1,2], [4,1,2,3]

```cpp
class Solution {
public:
    /**
     * @param nums: An integer array
     * @return: nothing
     */
    void recoverRotatedSortedArray(vector<int> &nums) {
		int maxindex = -1;
		int size = nums.size();
		for (int i = 0; i < size - 1; i++) {
			if (nums[i] > nums[i + 1]) {
				maxindex = i;
				break;
			}
		}
		if (maxindex == -1) {
			return;
		}
		vector<int>temp;
		for (int i = maxindex + 1; i < size; i++) {
			temp.push_back(nums[i]);
		}
		for (int i = 0; i <= maxindex; i++) {
			temp.push_back(nums[i]);
		}
		nums = temp;
		return;
    }
};
```

# 40. 用栈实现队列

正如标题所述，你需要使用两个栈来实现队列的一些操作。

队列应支持push(element)，pop() 和 top()，其中pop是弹出队列中的第一个(最前面的)元素。

pop和top方法都应该返回第一个元素的值。

### 样例

**例1:**

```
输入:
    push(1)
    pop()    
    push(2)
    push(3)
    top()    
    pop()     
输出:
    1
    2
    2
```

**例2:**

```
输入:
    push(1)
    push(2)
    push(2)
    push(3)
    push(4)
    push(5)
    push(6)
    push(7)
    push(1)
输出:
[]
```

### 挑战

仅使用两个栈来实现它，不使用任何其他数据结构，push，pop 和 top的复杂度都应该是均摊O(1)的

### 注意事项

假设调用pop()函数的时候，队列非空

```cpp
class MyQueue {
public:
    stack<int> stk;
    MyQueue() {
        // do intialization if necessary
    }

    /*
     * @param element: An integer
     * @return: nothing
     */
    void push(int element) {
        stk.push(element);
    }

    /*
     * @return: An integer
     */
    int pop() {
        stack<int> temp;
        int size=stk.size();
        for(int i=0;i<size;i++){
            temp.push(stk.top());
            stk.pop();
        }
        int res=temp.top();
        temp.pop();
        size=temp.size();
        for(int i=0;i<size;i++){
            stk.push(temp.top());
            temp.pop();
        }
        return res;
    }

    /*
     * @return: An integer
     */
    int top() {
        stack<int> temp;
        int size=stk.size();
        for(int i=0;i<size;i++){
            temp.push(stk.top());
            stk.pop();
        }
        int res=temp.top();
        size=temp.size();
        for(int i=0;i<size;i++){
            stk.push(temp.top());
            temp.pop();
        }
        return res;
    }
};
```

### 41. 最大子数组

给定一个整数数组，找到一个具有最大和的子数组，返回其最大和。

### 样例

**样例1:**

```
输入：[−2,2,−3,4,−1,2,1,−5,3]
输出：6
解释：符合要求的子数组为[4,−1,2,1]，其最大和为 6。
```

**样例2:**

```
输入：[1,2,3,4]
输出：10
解释：符合要求的子数组为[1,2,3,4]，其最大和为 10。
```

### 挑战

要求时间复杂度为O(n)

### 注意事项

子数组最少包含一个数

```cpp
class Solution {
public:
    /**
     * @param nums: A list of integers
     * @return: A integer indicate the sum of max subarray
     */
    int maxSubArray(vector<int> &nums) {
        int sum = 0, maxAns = INT_MIN;
        for (int i = 0; i < nums.size(); ++i) {
            sum += nums[i];
            maxAns = max(maxAns, sum);
            sum = max(sum, 0);
        }
        return maxAns;
    }
};
```

# 44. 最小子数组

给定一个整数数组，找到一个具有最小和的连续子数组。返回其最小和。

### 样例

**样例 1**

```
输入：[1, -1, -2, 1]
输出：-3
```

**样例 2**

```
输入：[1, -1, -2, 1, -4]
输出：-6
```

### 注意事项

子数组最少包含一个数字

```cpp
class Solution {
public:
    /*
     * @param nums: a list of integers
     * @return: A integer indicate the sum of minimum subarray
     */
	int minSubArray(vector<int>& nums) {
		int s = nums[0], minsum = s;
		for (int i = 1; i < nums.size(); i++) {
			s = min(0, s) + nums[i];
			minsum = min(minsum, s);
		}
		return minsum;
	}
};
```

# 46. 主元素

给定一个整型数组，找出主元素，它在数组中的出现次数严格大于数组元素个数的二分之一。



### 样例

**样例 1:**

```
输入: [1, 1, 1, 1, 2, 2, 2]
输出: 1
```

**样例 2:**

```
输入: [1, 1, 1, 2, 2, 2, 2]
输出: 2
```

### 挑战

要求时间复杂度为O(n)，空间复杂度为O(1)

### 注意事项

你可以假设数组非空，且数组中总是存在主元素。

```cpp
class Solution {
public:
    /*
     * @param nums: a list of integers
     * @return: find a  majority number
     */
    int majorityNumber(vector<int> &nums) {
		vector<pair<int, int>>count;
		pair<int, int>temp(nums[0], 1);
		count.push_back(temp);
		for (int i = 1; i < nums.size(); i++) {
			int flags = 0;
			for (int j = 0; j < count.size(); j++) {
				if (nums[i] == count[j].first) {
					flags = 1;
					count[j].second++;
				}
			}
			if (flags == 0) {
				temp.first = nums[i];
				temp.second = 1;
				count.push_back(temp);
			}
		}
		double size = nums.size() / 2.0;
		for (int i = 0; i < count.size(); i++) {
			if (count[i].second > size) {
				return count[i].first;
			}
		}
    }
};
```

# 50. 数组剔除元素后的乘积

给定一个整数数组A。
定义`B[i] = A[0] * ... * A[i-1] * A[i+1] * ... * A[n-1]`， 计算B的时候请不要使用除法。请输出B。

### 样例

**样例 1**

```
输入: A = [1, 2, 3]
输出: [6, 3, 2]
解析：B[0] = A[1] * A[2] = 6; B[1] = A[0] * A[2] = 3; B[2] = A[0] * A[1] = 2
```

**样例 2**

```
输入: A = [2, 4, 6]
输出: [24, 12, 8]
```

```cpp
class Solution {
public:
    /*
     * @param nums: Given an integers array A
     * @return: A long long array B and B[i]= A[0] * ... * A[i-1] * A[i+1] * ... * A[n-1]
     */
    vector<long long> productExcludeItself(vector<int> &nums) {
		vector<long long>res;
		for (int i = 0; i < nums.size(); i++) {
			long long temp = 1;
			for (int j = 0; j < nums.size(); j++) {
				if (i != j) {
					temp *= nums[j];
				}
			}
			res.push_back(temp);
		}
		return res;
    }
};
```

# 52. 下一个排列

给定一个整数数组来表示排列，找出其之后的一个排列。

### 样例

例1:

```
输入:[1]
输出:[1]
```

例2:

```
输入:[1,3,2,3]
输出:[1,3,3,2]
```

例3:

```
输入:[4,3,2,1]
输出:[1,2,3,4]
```

### 注意事项

排列中可能包含重复的整数

```cpp
class Solution {
public:
    /**
     * @param nums: A list of integers
     * @return: A list of integers
     */
    vector<int> nextPermutation(vector<int> &nums) {
        if(nums.size()==1){
            return nums;
        }
        int i=nums.size()-2;
        while(i>=0 and nums[i]>=nums[i+1]){
            i--;
        }
        int j=nums.size()-1;
        if(i>=0){
            while(nums[j]<=nums[i]){
                j--;
            }
            swap(nums[i],nums[j]);
        }
        reverse(nums.begin()+i+1,nums.end());
        return nums;
    }
};
```



# 53. 翻转字符串中的单词

给定一个字符串，逐个翻转字符串中的每个单词。

### 样例

```
样例  1:
	输入:  "the sky is blue"
	输出:  "blue is sky the"
	
	样例解释: 
	返回逐字反转的字符串.

样例 2:
	输入:  "hello world"
	输出:  "world hello"
	
	样例解释: 
	返回逐字反转的字符串.
```

### 说明



-    单词的构成：无空格字母构成一个单词，有些单词末尾会带有标点符号
-    输入字符串是否包括前导或者尾随空格？可以包括，但是反转后的字符不能包括
-    如何处理两个单词间的多个空格？在反转字符串中间空格减少到只含一个

```cpp
class Solution {
public:
    /*
     * @param s: A string
     * @return: A string
     */
	string reverseWords(string& s) {
		if (s.find_first_not_of(' ') == string::npos) {
			return "";
		}
		string res;
		int i = s.length() - 1;
		do {
			vector<char>temp;
			for (; i >= 0 and s[i] != ' '; i--) {
				temp.push_back(s[i]);
			}
			i--;
			reverse(temp.begin(), temp.end());
			if (temp.size() > 0) {
				for (int j = 0; j < temp.size(); j++) {
					res += temp[j];
				}
				res += ' ';
			}
		} while (i >= 0);
		return res;
	}
};
```

# 55. 比较字符串

比较两个字符串A和B，确定A中是否包含B中所有的字符。字符串A和B中的字符都是 **大写字母**

### 样例

给出 A = `"ABCD"` B = `"ACD"`，返回 `true`

给出 A = `"ABCD"` B = `"AABC"`， 返回 `false`

### 注意事项

在 A 中出现的 B 字符串里的字符不需要连续或者有序。

```cpp
class Solution {
public:
    /**
     * @param A: A string
     * @param B: A string
     * @return: if string A contains all of the characters in B return true else return false
     */
	bool compareStrings(string& A, string& B) {
		for (int i = 0; i < B.size(); i++) {
			bool find = false;
			for (int j = 0; j < A.size(); j++) {
				if (A[j] == B[i]) {
					A.erase(A.begin() + j);
					find = true;
					break;
				}
			}
			if (!find) {
				return false;
			}
		}
		return true;
	}
};
```

# 56. 两数之和

给一个整数数组，找到两个数使得他们的和等于一个给定的数 *target*。

你需要实现的函数`twoSum`需要返回这两个数的下标, 并且第一个下标小于第二个下标。注意这里下标的范围是 0 到 *n-1*。

### 样例

```
样例1:
给出 numbers = [2, 7, 11, 15], target = 9, 返回 [0, 1].
样例2:
给出 numbers = [15, 2, 7, 11], target = 9, 返回 [1, 2].
```

### 挑战

给自己加点挑战

-    O(n)*O*(*n*) 空间复杂度，O(nlogn)*O*(*n**l**o**g**n*) 时间复杂度，
-    O(n)*O*(*n*) 空间复杂度，O(n)*O*(*n*) 时间复杂度，

### 注意事项

你可以假设只有一组答案。

```cpp
class Solution {
public:
    /**
     * @param numbers: An array of Integer
     * @param target: target = numbers[index1] + numbers[index2]
     * @return: [index1 + 1, index2 + 1] (index1 < index2)
     */
    vector<int> twoSum(vector<int> &numbers, int target) {
		vector<int>res;
		size_t size = numbers.size();
		for (int i = 0; i < size; ++i) {
			for (int j = i + 1; j < size; ++j) {
				if (target == numbers[i] + numbers[j]) {
					res.push_back(i);
					res.push_back(j);
					return res;
				}
			}
		}
    }
};
```

# 60. 搜索插入位置

给定一个排序数组和一个目标值，如果在数组中找到目标值则返回索引。如果没有，返回到它将会被按顺序插入的位置。

你可以假设在数组中无重复元素。

### 样例

**[1,3,5,6]**，5 → 2

**[1,3,5,6]**，2 → 1

**[1,3,5,6]**， 7 → 4

**[1,3,5,6]**，0 → 0

### 挑战

时间复杂度为O(log(n))

```cpp
class Solution {
public:
    /**
     * @param A: an integer sorted array
     * @param target: an integer to be inserted
     * @return: An integer
     */
    int searchInsert(vector<int> &A, int target) {
        if(A.size()==0){
            return 0;
        }
        for(int i=0;i<A.size();i++){
            if(A[i]>=target){
                return i;
            }
        }
        return A.size();
    }
};
```

# 64. 合并排序数组（简单版）

合并两个排序的整数数组A和B变成一个新的数组。

### 样例

**样例 1:**

```
输入：[1, 2, 3]  3  [4,5]  2
输出：[1,2,3,4,5]
解释:
经过合并新的数组为[1,2,3,4,5]
```

**样例 2:**

```
输入：[1,2,5] 3 [3,4] 2
输出：[1,2,3,4,5]
解释：
经过合并新的数组为[1,2,3,4,5]
```

### 注意事项

你可以假设A具有足够的空间（A数组的大小大于或等于m+n）去添加B中的元素。

```cpp
class Solution {
public:
    /*
     * @param A: sorted integer array A which has m elements, but size of A is m+n
     * @param m: An integer
     * @param B: sorted integer array B which has n elements
     * @param n: An integer
     * @return: nothing
     */
    void mergeSortedArray(int A[], int m, int B[], int n) {
        for(int i=0;i<n;i++){
            A[m+i]=B[i];
        }
        sort(A,A+m+n,less<int>());
        return;
    }
};
```

# 66.  二叉树的前序遍历

描述

给出一棵二叉树，返回其节点值的前序遍历。

首个数据为根节点，后面接着是其左儿子和右儿子节点值，"#"表示不存在该子节点。节点数量不超过20

样例

**样例 1:**

```
输入：{1,2,3}
输出：[1,2,3]
解释：
   1
  / \
 2   3
它将被序列化为{1,2,3}
前序遍历
```

**样例 2:**

```
输入：{1,#,2,3}
输出：[1,2,3]
解释：
1
 \
  2
 /
3
它将被序列化为{1,#,2,3}
前序遍历
```

挑战

你能使用非递归实现么？

```cpp
/**
 * Definition of TreeNode:
 * class TreeNode {
 * public:
 *     int val;
 *     TreeNode *left, *right;
 *     TreeNode(int val) {
 *         this->val = val;
 *         this->left = this->right = NULL;
 *     }
 * }
 */

class Solution {
public:
    /**
     * @param root: A Tree
     * @return: Preorder in ArrayList which contains node values.
     */
    vector<int>preorder;
    void traverse(TreeNode*root){
        if(root==NULL){
            return;
        }
        preorder.push_back(root->val);
        traverse(root->left);
        traverse(root->right);
    }
    vector<int> preorderTraversal(TreeNode * root) {
        preorder.clear();
        traverse(root);
        return preorder;
    }
};
```

# 67.  二叉树的中序遍历

描述

给出一棵二叉树,返回其中序遍历

样例

**样例 1:**

```
输入：{1,2,3}
输出：[2,1,3]
解释：
   1
  / \
 2   3
它将被序列化为{1,2,3}
中序遍历
```

**样例 2:**

```
输入：{1,#,2,3}
输出：[1,3,2]
解释：
1
 \
  2
 /
3
它将被序列化为{1,#,2,3}
中序遍历
```

```cpp
/**
 * Definition of TreeNode:
 * class TreeNode {
 * public:
 *     int val;
 *     TreeNode *left, *right;
 *     TreeNode(int val) {
 *         this->val = val;
 *         this->left = this->right = NULL;
 *     }
 * }
 */

class Solution {
public:
    /**
     * @param root: A Tree
     * @return: Inorder in ArrayList which contains node values.
     */
    vector<int>res;
    void traversal(TreeNode* root){
        while(root==NULL){
            return;
        }
        traversal(root->left);
        res.push_back(root->val);
        traversal(root->right);
    }
    vector<int> inorderTraversal(TreeNode * root) {
        res.clear();
        traversal(root);
        return res;
    }
};
```



# 68. 二叉树的后序遍历

描述

给出一棵二叉树，返回其节点值的前序遍历。

首个数据为根节点，后面接着是其左儿子和右儿子节点值，"#"表示不存在该子节点。节点数量不超过20

样例

**样例 1:**

```
输入：{1,2,3}
输出：[1,2,3]
解释：
   1
  / \
 2   3
它将被序列化为{1,2,3}
前序遍历
```

**样例 2:**

```
输入：{1,#,2,3}
输出：[1,2,3]
解释：
1
 \
  2
 /
3
它将被序列化为{1,#,2,3}
前序遍历
```

挑战

你能使用非递归实现么？

```cpp
/**
 * Definition of TreeNode:
 * class TreeNode {
 * public:
 *     int val;
 *     TreeNode *left, *right;
 *     TreeNode(int val) {
 *         this->val = val;
 *         this->left = this->right = NULL;
 *     }
 * }
 */

class Solution {
public:
    /**
     * @param root: A Tree
     * @return: Preorder in ArrayList which contains node values.
     */
    vector<int>preorder;
    void traverse(TreeNode*root){
        if(root==NULL){
            return;
        }
        preorder.push_back(root->val);
        traverse(root->left);
        traverse(root->right);
    }
    vector<int> preorderTraversal(TreeNode * root) {
        preorder.clear();
        traverse(root);
        return preorder;
    }
};
```



# 75. 寻找峰值

你给出一个整数数组(size为n)，其具有以下特点：

-    相邻位置的数字是不同的
-    A[0] < A[1] 并且 A[n - 2] > A[n - 1]

假定*P*是峰值的位置则满足`A[P] > A[P-1]`且`A[P] > A[P+1]`，返回数组中任意一个峰值的位置。

### 样例

```
样例 1:
	输入:  [1, 2, 1, 3, 4, 5, 7, 6]
	输出:  1 or 6
	
	解释:
	返回峰顶元素的下标


样例 2:
	输入: [1,2,3,4,1]
	输出:  3
```

### 挑战

时间复杂度O (logN)

### 注意事项

-    数组保证至少存在一个峰
-    如果数组存在多个峰，返回其中任意一个就行
-    数组至少包含 3 个数

```cpp
class Solution {
public:
    /**
     * @param A: An integers array.
     * @return: return any of peek positions.
     */
    int findPeak(vector<int> &A) {
        int l=1,r=A.size();
        while(l<=r){
            int mid=(l+r)/2;
            if(A[mid]>A[mid-1] and A[mid]>A[mid+1]){
                return mid;
            }
            if(A[mid]>A[mid-1]){
                l=mid+1;
            }
            else{
                r=mid-1;
            }
        }
        return -1;
    }
};
```

# 76. 最长上升子序列

给定一个整数序列，找到最长上升子序列（LIS），返回LIS的长度。

### 样例

```
样例 1:
	输入:  [5,4,1,2,3]
	输出:  3
	
	解释:
	LIS 是 [1,2,3]


样例 2:
	输入: [4,2,4,5,3,7]
	输出:  4
	
	解释: 
	LIS 是 [2,4,5,7]
```

### 挑战

要求时间复杂度为O(n^2) 或者 O(nlogn)

### 说明

最长上升子序列的定义：

最长上升子序列问题是在一个无序的给定序列中找到一个尽可能长的由低到高排列的子序列，这种子序列不一定是连续的或者唯一的。
https://en.wikipedia.org/wiki/Longest_increasing_subsequence

```cpp
class Solution {
public:
    int longestIncreasingSubsequence(vector<int> &nums) {
        if (nums.size() == 0) {
            return 0;
        }
        int res = 1;
        vector<int> LIS(nums.size(), 1);
        for (int i = 1; i < nums.size(); ++i) {
            for (int j = 0; j < i; ++j) {
                if (nums[i] > nums[j]) {
                    LIS[i] = max(LIS[i], LIS[j] + 1);
                }
            }
            res = max(res, LIS[i]);
        }
        return res;
    }
};
```

# 80. 中位数

给定一个未排序的整数数组，找到其中位数。

中位数是排序后数组的中间值，如果数组的个数是偶数个，则返回排序后数组的第N/2个数。

### 样例

**样例 1:**

```
输入：[4, 5, 1, 2, 3]
输出：3
解释：
经过排序，得到数组[1,2,3,4,5]，中间数字为3
```

**样例 2:**

```
输入：[7, 9, 4, 5]
输出：5
解释：
经过排序，得到数组[4,5,7,9]，第二个(4/2)数字为5
```

### 挑战

时间复杂度为O(n)

### 注意事项

数组大小不超过10000

```cpp
class Solution {
public:
    /**
     * @param nums: A list of integers
     * @return: An integer denotes the middle number of the array
     */
    int median(vector<int> &nums) {
		sort(nums.begin(), nums.end());
		if (nums.size() % 2 == 0) {
			return nums[(nums.size() / 2) - 1];
		}
		else {
			return nums[nums.size() / 2];
		}
    }
};
```

# 82. 落单的数

给出 `2 * n + 1`个数字，除其中一个数字之外其他每个数字均出现两次，找到这个数字。

### 样例

**样例 1:**

```
输入：[1,1,2,2,3,4,4]
输出：3
解释：
仅3出现一次
```

**样例 2:**

```
输入：[0,0,1]
输出：1
解释：
仅1出现一次
```

### 挑战

一次遍历，常数级的额外空间复杂度

### 注意事项

-    n≤100

```cpp
class Solution {
public:
    /**
     * @param A: An integer array
     * @return: An integer
     */
    int singleNumber(vector<int> &A) {
		vector<pair<int, int>>count;
		pair<int, int>temp;
		temp.first = A[0];
		temp.second = 1;
		count.push_back(temp);
		for (int i = 1; i < A.size(); i++) {
			bool flag = true;
			for (int j = 0; j < count.size(); j++) {
				if (count[j].first == A[i]) {
					count[j].second++;
					flag = false;
					break;
				}
			}
			if (flag) {
				temp.first = A[i];
				temp.second = 1;
				count.push_back(temp);
			}
		}
		for (int i = 0; i < count.size(); i++) {
			if (count[i].second == 1) {
				return count[i].first;
			}
		}
    }
};
```

# 93.  平衡二叉树

描述

给定一个二叉树,确定它是高度平衡的。对于这个问题,一棵高度平衡的二叉树的定义是：一棵二叉树中每个节点的两个子树的深度相差不会超过1。 

样例

```
样例  1:
	输入: tree = {1,2,3}
	输出: true
	
	样例解释:
	如下，是一个平衡的二叉树。
		  1  
		 / \                
		2  3

	
样例  2:
	输入: tree = {3,9,20,#,#,15,7}
	输出: true
	
	样例解释:
	如下，是一个平衡的二叉树。
		  3  
		 / \                
		9  20                
		  /  \                
		 15   7 

	
样例  2:
	输入: tree = {1,#,2,3,4}
	输出: false
	
	样例解释:
	如下，是一个不平衡的二叉树。1的左右子树高度差2
		  1  
		   \                
		   2                
		  /  \                
		 3   4
	
```

```cpp
/**
 * Definition of TreeNode:
 * class TreeNode {
 * public:
 *     int val;
 *     TreeNode *left, *right;
 *     TreeNode(int val) {
 *         this->val = val;
 *         this->left = this->right = NULL;
 *     }
 * }
 */

class Solution {
public:
    /**
     * @param root: The root of binary tree.
     * @return: True if this Binary tree is Balanced, or false.
     */
    bool isBalanced(TreeNode * root) {
        return dfs(root).first;
    }
    pair<bool,int>dfs(TreeNode*root){
        if(!root){
            return {true,0};
        }
        auto l=dfs(root->left);
        auto r=dfs(root->right);
        pair<bool,int>ans={true,max(l.second,r.second)+1};
        ans.first&=l.first&&r.first &&(abs(l.second-r.second)<=1);
        return ans;
    }
};
```



# 100. 删除排序数组中的重复数字

给定一个排序数组，在原数组中“删除”重复出现的数字，使得每个元素只出现一次，并且返回“新”数组的长度。

不要使用额外的数组空间，必须在不使用额外空间的条件下原地完成。

### 样例

**样例 1:**

```
输入:  []
输出: 0
```

**样例 2:**

```
输入:  [1,1,2]
输出: 2	
解释:  数字只出现一次的数组为: [1,2]
```

```
class Solution {
public:
    /*
     * @param nums: An ineger array
     * @return: An integer
     */
    int removeDuplicates(vector<int> &nums) {
        vector<int>::iterator iter=unique(nums.begin(),nums.end());
        nums.erase(iter,nums.end());
        return nums.size();
    }
};
```

# 101. 删除排序数组中的重复数字 II

给你一个排序数组，删除其中的重复元素，使得每个数字最多出现两次，返回新的数组的长度。
如果一个数字出现超过2次，则这个数字最后保留两个。

### 样例

```
样例 1:
	输入: []
	输出: 0


样例 2:
	输入:  [1,1,1,2,2,3]
	输出: 5
	
	样例解释: 
	长度为 5，  数组为：[1,1,2,2,3]
```

### 注意事项

需要在原数组中操作

```cpp
class Solution {
public:
    /**
     * @param A: a list of integers
     * @return : return an integer
     */
    int removeDuplicates(vector<int> &nums) {
        if(nums.size()==0){
            return 0;
        }
        bool equal=false;
        for(int i=1;i<nums.size();){
            if(nums[i]==nums[i-1] and equal==false){
                equal=true;
                ++i;
            }
            else if(nums[i]!=nums[i-1]){
                equal=false;
                ++i;
            }
            else{
                nums.erase(nums.begin()+i);
            }
        }
        return nums.size();
    }
};
```

# 110. 最小路径和

给定一个只含非负整数的m*n网格，找到一条从左上角到右下角的可以使数字和最小的路径。



### 样例

样例 1:

```
输入:  [[1,3,1],[1,5,1],[4,2,1]]
输出: 7	
样例解释：
路线为： 1 -> 3 -> 1 -> 1 -> 1。
```

样例 2:

```
输入:  [[1,3,2]]
输出:  6
解释:  
路线是： 1 -> 3 -> 2
```

### 注意事项

你在同一时间只能向下或者向右移动一步

```cpp
class Solution {
public:
    /**
     * @param grid: a list of lists of integers
     * @return: An integer, minimizes the sum of all numbers along its path
     */
    int minPathSum(vector<vector<int>> &grid) {
        int f[1000][1000];
        if(grid.size()==0 or grid[0].size()==0){
            return 0;
        }
        f[0][0]=grid[0][0];
        for(int i=0;i<grid.size();i++){
            f[i][0]=f[i-1][0]+grid[i][0];
        }
        for(int i=1;i<grid[0].size();i++){
            f[0][i]=f[0][i-1]+grid[0][i];
        }
        for(int i=1;i<grid.size();i++){
            for(int j=1;j<grid[0].size();j++){
                f[i][j]=min(f[i-1][j],f[i][j-1])+grid[i][j];
            }
        }
        return f[grid.size()-1][grid[0].size()-1];
    }
};
```

# 111. 爬楼梯

假设你正在爬楼梯，需要n步你才能到达顶部。但每次你只能爬一步或者两步，你能有多少种不同的方法爬到楼顶部？

### 样例

```
样例 1:
	输入:  n= 3
	输出: 3
	
	样例解释：
	1) 1, 1, 1
	2) 1, 2
	3) 2, 1
	共3种


样例 2:
	输入:  n = 1
	输出: 1
	
	解释:  
	只有一种方案
```

```cpp
class Solution {
public:
    /**
     * @param n: An integer
     * @return: An integer
     */
    int climbStairs(int n) {
        int a=min(n,1);
        for(auto i=1,b=a;i<n;++i,b=a-b){
            a+=b;
        }
        return a;
    }
};
```

# 112. 删除排序链表中的重复元素

给定一个排序链表，删除所有重复的元素每个元素只留下一个。

### 样例

```
样例 1:
	输入:  null
	输出: null


样例 2:
	输入: 1->1->2->null
	输出: 1->2->null

样例 3:
	输入: 1->1->2->3->3->null
	输出: 1->2->3->null
```

```cpp
/**
 * Definition of singly-linked-list:
 * class ListNode {
 * public:
 *     int val;
 *     ListNode *next;
 *     ListNode(int val) {
 *        this->val = val;
 *        this->next = NULL;
 *     }
 * }
 */

class Solution {
public:
    /**
     * @param head: head is the head of the linked list
     * @return: head of linked list
     */
    ListNode * deleteDuplicates(ListNode * head) {
        ListNode *res=head;
        if(head==nullptr){
            return head;
        }
        for(ListNode *reshead=nullptr;head->next!=NULL;){
            reshead=head->next;
            if(head->val==reshead->val){
                head->next=reshead->next;
            }else{
                head=head->next;
            }
        }
        return res;
    }
};
```

# 114. 不同的路径

有一个机器人的位于一个 *m* × *n* 个网格左上角。

机器人每一时刻只能向下或者向右移动一步。机器人试图达到网格的右下角。

问有多少条不同的路径？

### 样例

**样例 1:**

```
输入: n = 1, m = 3
输出: 1	
解释: 只有一条通往目标位置的路径。
```

**样例 2:**

```
输入:  n = 3, m = 3
输出: 6	
解释:
	D : Down
	R : Right
	1) DDRR
	2) DRDR
	3) DRRD
	4) RRDD
	5) RDRD
	6) RDDR
```

### 注意事项

n和m均不超过100
且答案保证在32位整数可表示范围内。

```cpp
class Solution {
public:
    /**
     * @param m: positive integer (1 <= m <= 100)
     * @param n: positive integer (1 <= n <= 100)
     * @return: An integer
     */
	int uniquePaths(int m, int n) {
		vector<vector<int>>count(m, vector<int>(n, 1));
		for (int i = m - 2; i >= 0; --i) {
			for (int j = n - 2; j >= 0; --j) {
				count[i][j] = count[i + 1][j] + count[i][j + 1];
			}
		}
		return count[0][0];
	}
};
```

# 117. 跳跃游戏 II

给出一个非负整数数组，你最初定位在数组的第一个位置。

数组中的每个元素代表你在那个位置可以跳跃的最大长度。　　　

你的目标是使用最少的跳跃次数到达数组的最后一个位置。

### 样例

***样例 1***

```
输入 : [2,3,1,1,4]
输出 : 2
解释 : 到达最后位置的最小跳跃次数是2(从下标0到1跳跃1个距离长度，然后跳跃3个距离长度到最后位置)
```

```cpp
class Solution {
public:
    /**
     * @param A: A list of integers
     * @return: An integer
     */
    int jump(vector<int> &A) {
        int n=A.size();
        vector<int>dp(n);
        dp[0]=0;
        for(int i=1;i<n;i++){
            dp[i]=INT_MAX;
            for(int j=0;j<i;j++){
                if(A[j]+j>=i){
                    dp[i]=min(dp[i],dp[j]+1);
                }
            }
        }
        return dp[n-1];
    }
};
```

# 125. 背包问题 II

有 `n` 个物品和一个大小为 `m` 的背包. 给定数组 `A` 表示每个物品的大小和数组 `V` 表示每个物品的价值.

问最多能装入背包的总价值是多大?

### 样例

**样例 1:**

```
输入: m = 10, A = [2, 3, 5, 7], V = [1, 5, 2, 4]
输出: 9
解释: 装入 A[1] 和 A[3] 可以得到最大价值, V[1] + V[3] = 9 
```

**样例 2:**

```
输入: m = 10, A = [2, 3, 8], V = [2, 5, 8]
输出: 10
解释: 装入 A[0] 和 A[2] 可以得到最大价值, V[0] + V[2] = 10
```

### 挑战

O(nm) 空间复杂度可以通过, 不过你可以尝试 O(m) 空间复杂度吗?

### 注意事项

1.   `A[i], V[i], n, m` 均为整数
2.   你不能将物品进行切分
3.   你所挑选的要装入背包的物品的总大小不能超过 `m`
4.   每个物品只能取一次

```cpp
class Solution {
public:
    /**
     * @param m: An integer m denotes the size of a backpack
     * @param A: Given n items with size A[i]
     * @param V: Given n items with value V[i]
     * @return: The maximum value
     */
    int backPackII(int m, vector<int> &A, vector<int> &V) {
        vector<int>f(m+1,0);
        for(int i=0;i<A.size();i++){
            for(int j=m;j>=A[i];j--){
                f[j]=max(f[j],f[j-A[i]]+V[i]);
            }
        }
        return f[m];
    }
};
```

# 128. 哈希函数

在数据结构中，哈希函数是用来将一个字符串（或任何其他类型）转化为小于哈希表大小且大于等于零的整数。一个好的哈希函数可以尽可能少地产生冲突。一种广泛使用的哈希函数算法是使用数值33，假设任何字符串都是基于33的一个大整数，比如：

hashcode("abcd") = (ascii(a) * 333 + ascii(b) * 332 + ascii(c) *33 + ascii(d)) % HASH_SIZE 

​               = (97* 333 + 98 * 332 + 99 * 33 +100) % HASH_SIZE

​               = 3595978 % HASH_SIZE

其中HASH_SIZE表示哈希表的大小(可以假设一个哈希表就是一个索引0 ~ HASH_SIZE-1的数组)。

给出一个字符串作为key和一个哈希表的大小，返回这个字符串的哈希值。

### 样例

**样例 1:**

```
输入:  key = "abcd", size = 1000
输出: 978	
样例解释：(97 * 33^3 + 98*33^2 + 99*33 + 100*1)%1000 = 978
```

**样例 2:**

```
输入:  key = "abcd", size = 100
输出: 78	
样例解释：(97 * 33^3 + 98*33^2 + 99*33 + 100*1)%100 = 78
```

### 说明

对于这个问题，您没有必要设计自己的哈希算法或考虑任何冲突问题，您只需要按照描述实现算法.

```cpp
class Solution {
public:
    /**
     * @param key: A string you should hash
     * @param HASH_SIZE: An integer
     * @return: An integer
     */
    int hashCode(string &key, int HASH_SIZE) {
		vector<long long>hash;
		hash.push_back(1);
		for (int i = 1; i < key.size(); i++) {
			hash.push_back((hash[i - 1] * 33) % HASH_SIZE);
		}
		long long res = 0;
		for (int i = 0; i < key.size(); i++) {
			res += int(key[i]) * hash[key.size() - 1 - i];
			res %= HASH_SIZE;
		}
		return res;
    }
};
```

# 133. 最长单词

给一个词典，找出其中所有最长的单词。

### 样例

```
样例 1:
	输入:   {
		"dog",
		"google",
		"facebook",
		"internationalization",
		"blabla"
		}
	输出: ["internationalization"]



样例 2:
	输入: {
		"like",
		"love",
		"hate",
		"yes"		
		}
	输出: ["like", "love", "hate"]
```

### 挑战

遍历两次的办法很容易想到，如果只遍历一次你有没有什么好办法？

```cpp
class Solution {
public:
    /*
     * @param dictionary: an array of strings
     * @return: an arraylist of strings
     */
    vector<string> longestWords(vector<string> &dictionary) {
		vector<string>res;
		res.push_back(dictionary[0]);
		vector<string>::iterator iter;
		for (iter = dictionary.begin() + 1; iter != dictionary.end(); ++iter) {
			if (iter->size() > res[0].size()) {
				res.clear();
				res.push_back(*iter);
			}
			else if (iter->size() == res[0].size()) {
				res.push_back(*iter);
			}
		}
		return res;
    }
};
```

# 138. 子数组之和

给定一个整数数组，找到和为 0 的子数组。你的代码应该返回满足要求的子数组的起始位置和结束位置

### 样例

**样例 1:**

```
输入: [-3, 1, 2, -3, 4]
输出: [0,2] 或 [1,3]	
样例解释： 返回任意一段和为0的区间即可。
```

**样例 2:**

```
输入: [-3, 1, -4, 2, -3, 4]
输出: [1,5]
```

### 注意事项

至少有一个子数组的和为 0

```cpp
class Solution {
public:
    /**
     * @param nums: A list of integers
     * @return: A list of integers includes the index of the first number and the index of the last number
     */
    vector<int> subarraySum(vector<int> &nums) {
		vector<int>result;
		unordered_map<int, int>hash;
		hash[0] = -1;
		int sum = 0;
		for (int i = 0; i < nums.size(); i++) {
			//累加前缀和
			sum += nums[i];
			//前缀和曾经出现，即这个区间的和为0
			if (hash.find(sum) != hash.end()) {
				result.push_back(hash[sum] + 1);
				result.push_back(i);
				break;
			}
			//前缀和第一次出现，存入hash
			hash[sum] = i;
		}
		return result;
    }
};
```

# 141. 对x开根

实现 `int sqrt(int x)` 函数，计算并返回 *x* 的平方根。

### 样例

```
样例 1:
	输入:  0
	输出: 0


样例 2:
	输入: 3
	输出: 1
	
	样例解释：
	返回对x开根号后向下取整的结果。

样例 3:
	输入: 4
	输出: 2
```

### 挑战

```cpp
class Solution {
public:
    /**
     * @param x: An integer
     * @return: The sqrt of x
     */
    int sqrt(int x) {
        long long res=1+x/2,del=res;
        for(;abs(del=res*res-x)>=res*2;res-=del/2/res);
        return del>0?--res:res;
    }
};
```

# 142. O(1)时间检测2的幂次

用 O(*1*) 时间检测整数 *n* 是否是 *2* 的幂次。

### 样例

`n=4`，返回 `true`;

`n=5`，返回 `false`.

### 挑战

O(*1*) 时间复杂度

```cpp
class Solution {
public:
    /**
     * @param n: An integer
     * @return: True or false
     */
    bool checkPowerOf2(int n) {
        if(n==0){
            return false;
        }
        while(n%2==0){
            n/=2;
        }
        return n==1;
    }
};
```

# 145. 大小写转换

将一个字符由小写字母转换为大写字母

### 样例

**样例 1:**

```
输入: 'a'
输出: 'A'
```

**样例 2:**

```
输入: 'b'
输出: 'B'
```

### 注意事项

你可以假设输入一定在小写字母 a ~ z 之间

```cpp
class Solution {
public:
    /**
     * @param character: a character
     * @return: a character
     */
    char lowercaseToUppercase(char character) {
		character = toupper(character);
		return character;
    }
};
```

# 148. 颜色分类

给定一个包含红，白，蓝且长度为 n 的数组，将数组元素进行分类使相同颜色的元素相邻，并按照红、白、蓝的顺序进行排序。

我们可以使用整数 0，1 和 2 分别代表红，白，蓝。

### 样例

***样例 1***

```
输入 : [1, 0, 1, 2]
输出 : [0, 1, 1, 2]
解释 : 原地排序。
```

### 挑战

一个相当直接的解决方案是使用计数排序扫描2遍的算法。

首先，迭代数组计算 0,1,2 出现的次数，然后依次用 0,1,2 出现的次数去覆盖数组。

你否能想出一个仅使用常数级额外空间复杂度且只扫描遍历一遍数组的算法？

### 注意事项

不能使用代码库中的排序函数来解决这个问题。
排序需要在原数组中进行。

```cpp
bool cmp(int a,int b){
    if(a<b){
        return true;
    }
    else{
        return false;
    }
}
class Solution {
public:
    /**
     * @param nums: A list of integer which is 0, 1 or 2 
     * @return: nothing
     */
    void sortColors(vector<int> &nums) {
        sort(nums.begin(),nums.end(),cmp);
    }
};
```

# 156. 合并区间

给出若干闭合区间，合并所有重叠的部分。

### 样例

**样例1:**

```
输入: [(1,3)]
输出: [(1,3)]
```

**样例 2:**

```
输入:  [(1,3),(2,6),(8,10),(15,18)]
输出: [(1,6),(8,10),(15,18)]
```

### 挑战

O(*n* log *n*) 的时间和 O(1) 的额外空间。

```cpp
class Solution {
public:
	/**
	 * @param intervals: interval list.
	 * @return: A new interval list.
	 */
	vector<Interval> merge(vector<Interval>& intervals) {
		if (intervals.size() == 1 or intervals.size() == 0) {
			return intervals;
		}
		Sort(intervals);
		vector<Interval>res;
		int left = intervals[0].start, right = intervals[0].end;
		for (int i = 1; i < intervals.size(); i++) {
			if (intervals[i].start < right and intervals[i].end>right) {
				right = intervals[i].end;
			}
			else if (intervals[i].start > right) {
				Interval temp(left, right);
				res.push_back(temp);
				left = intervals[i].start;
				right = intervals[i].end;
			}
			else if (intervals[i].start == right and left<intervals[i].end) {
				right = intervals[i].end;
			}
			if (i == intervals.size() - 1) {
				Interval temp(left, right);
				res.push_back(temp);
			}
		}
		return res;
	}
	void Sort(vector<Interval>& intervals) {
		for (int i = 0; i < intervals.size(); i++) {
			for (int j = 0; j < intervals.size() - 1 - i; j++) {
				if (intervals[j].start > intervals[j + 1].start) {
					swap(intervals[j], intervals[j + 1]);
				}
			}
		}
	}
};
```

# 157. 判断字符串是否没有重复字符

实现一个算法确定字符串中的字符是否均唯一出现

### 样例

**样例 1:**

```
输入:  "abc_____"
输出:  false
```

**样例 2:**

```
输入:  "abc"
输出:  true	
```

### 挑战

如果不使用额外的存储空间，你的算法该如何改变？

输入测试数据（每行一个参数）如何理解测试数据？

```cpp
class Solution {
public:
    /*
     * @param str: A string
     * @return: a boolean
     */
    bool isUnique(string &str) {
		char ascii[128] = { 0 };
		for (int i = 0; i < str.size(); i++) {
			if (ascii[str[i]] == 0) {
				ascii[str[i]] = 1;
			}
			else {
				return false;
			}
		}
		return true;
    }
};
```

# 158. 两个字符串是变位词

写出一个函数 `anagram(s, t)` 判断两个字符串是否可以通过改变字母的顺序变成一样的字符串。

### 样例

**样例 1:**

```
输入: s = "ab", t = "ab"
输出: true
```

**样例 2:**

```
输入:  s = "abcd", t = "dcba"
输出: true
```

**样例 3:**

```
输入:  s = "ac", t = "ab"
输出: false
```

### 挑战

O(n) 的时间复杂度, O(1) 的额外空间

### 说明

什么是 **Anagram**?

-    在更改字符顺序后两个字符串可以相同

```cpp
class Solution {
public:
    /**
     * @param s: The first string
     * @param t: The second string
     * @return: true or false
     */
    bool anagram(string &s, string &t) {
        sort(s.begin(),s.end());
        sort(t.begin(),t.end());
        if(s==t){
            return true;
        }
        else{
            return false;
        }
    }
};
```

# 165. 合并两个排序链表

描述

将两个排序（升序）链表合并为一个新的升序排序链表

样例

```
样例 1:
	输入: list1 = null, list2 = 0->3->3->null
	输出: 0->3->3->null


样例2:
	输入:  list1 =  1->3->8->11->15->null, list2 = 2->null
	输出: 1->2->3->8->11->15->null
```

```cpp
/**
 * Definition of singly-linked-list:
 * class ListNode {
 * public:
 *     int val;
 *     ListNode *next;
 *     ListNode(int val) {
 *        this->val = val;
 *        this->next = NULL;
 *     }
 * }
 */

class Solution {
public:
    /**
     * @param l1: ListNode l1 is the head of the linked list
     * @param l2: ListNode l2 is the head of the linked list
     * @return: ListNode head of linked list
     */
    ListNode * mergeTwoLists(ListNode * l1, ListNode * l2) {
        if(l1==NULL){
            return l2;
        }
        if(l2==NULL){
            return l1;
        }
        if(l1->val<l2->val){
            return sort(l1,l2);
        }
        else{
            return sort(l2,l1);
        }
    }

    ListNode * sort(ListNode * l1, ListNode * l2){
        ListNode*res=l1;
        ListNode*run=l1;
        l1=l1->next;
        do{
            if(l1->val<l2->val){
                run->next=l1;
                run=run->next;
                if(l1->next!=NULL){
                    l1=l1->next;
                }
                else{
                    run->next=l2;
                    break;
                }
            }
            else{
                run->next=l2;
                run=run->next;
                if(l2->next!=NULL){
                    l2=l2->next;
                }
                else{
                    run->next=l1;
                    break;
                }
            }   
        }while(1);
        return res;
    }
};
```



# 167. 链表求和

你有两个用链表代表的整数，其中每个节点包含一个数字。数字存储按照在原来整数中`相反`的顺序，使得第一个数字位于链表的开头。写出一个函数将两个整数相加，用链表形式返回和。

### 样例

**样例 1:**

```
输入: 7->1->6->null, 5->9->2->null
输出: 2->1->9->null	
样例解释: 617 + 295 = 912, 912 转换成链表:  2->1->9->null
```

**样例 2:**

```
输入:  3->1->5->null, 5->9->2->null
输出: 8->0->8->null	
样例解释: 513 + 295 = 808, 808 转换成链表: 8->0->8->null
```

```cpp
/**
 * Definition of singly-linked-list:
 * class ListNode {
 * public:
 *     int val;
 *     ListNode *next;
 *     ListNode(int val) {
 *        this->val = val;
 *        this->next = NULL;
 *     }
 * }
 */

class Solution {
public:
    /**
     * @param l1: the first list
     * @param l2: the second list
     * @return: the sum list of l1 and l2 
     */
    ListNode * addLists(ListNode * l1, ListNode * l2) {
		ListNode* result = nullptr, ** prev = &result;
		for (int carry = 0; l1 || l2 || carry;) {
			if (l1) {
				carry += l1->val;
				l1 = l1->next;
			}
			if (l2) {
				carry += l2->val;
				l2 = l2->next;
			}
			*prev = new ListNode(carry % 10);
			prev = &((*prev)->next);
			carry /= 10;
		}
		return result;
    }
};
```

# 172. 删除元素

给定一个数组和一个值，在原地删除与值相同的数字，返回新数组的长度。

元素的顺序可以改变，并且对新的数组不会有影响。

### 样例

给出一个数组 **[0,4,4,0,0,2,4,4]**，和值 4

返回 4 并且4个元素的新数组为**[0,0,0,2]**

```cpp
class Solution {
public:
    /*
     * @param A: A list of integers
     * @param elem: An integer
     * @return: The new length after remove
     */
    int removeElement(vector<int> &A, int elem) {
		for (int i = 0; i < A.size();) {
			if (A[i] == elem) {
				A.erase(A.begin() + i);
			}
			else {
				i++;
			}
		}
		return A.size();
    }
};
```

# 181. 将整数A转换为B

如果要将整数n转换为m，需要改变多少个bit位？

### 样例

```
样例 1:
	输入: n = 31, m = 14
	输出:  2
	
	解释:
	(11111) -> (01110) 需要改变两个位.


样例 2:
	输入: n = 1, m = 7
	输出:  2
	
	解释:
	(001) -> (111) 需要更改两位
```

### 注意事项

*n*和*m*均为32位整数。

```cpp
class Solution {
public:
    /**
     * @param a: An integer
     * @param b: An integer
     * @return: An integer
     */
	int bitSwapRequired(int a, int b) {
		vector<int>binarya(32, 0), binaryb(32, 0);
		if (a >= 0) {
			int i = 0;
			while (a != 0) {
				binarya[i] = a % 2;
				i++;
				a /= 2;
			}
		}
		else {
			a = abs(a);
			int i = 0;
			while (a != 0) {
				binarya[i] = a % 2;
				i++;
				a /= 2;
			}
			for (int j = 0; j < binarya.size(); j++) {
				if (binarya[j] == 0) {
					binarya[j] = 1;
				}
				else {
					binarya[j] = 0;
				}
			}
			for (int k = 0; k < binarya.size(); ++k) {
				if (binarya[k] == 0) {
					binarya[k] = 1;
					break;
				}
				else {
					binarya[k] = 0;
				}
			}
		}
		if (b >= 0) {
			int i = 0;
			while (b != 0) {
				binaryb[i] = b % 2;
				i++;
				b /= 2;
			}
		}
		else {
			b = abs(b);
			int i = 0;
			while (b != 0) {
				binaryb[i] = b % 2;
				i++;
				b /= 2;
			}
			for (int j = 0; j < binaryb.size(); j++) {
				if (binaryb[j] == 0) {
					binaryb[j] = 1;
				}
				else {
					binaryb[j] = 0;
				}
			}
			for (int k = 0; k < binaryb.size(); ++k) {
				if (binaryb[k] == 0) {
					binaryb[k] = 1;
					break;
				}
				else {
					binaryb[k] = 0;
				}
			}
		}
		int res = 0;
		for (int i = 0; i < 32; i++) {
			if (binarya[i] != binaryb[i]) {
				++res;
			}
		}
		return res;
	}
};
```

# 185.  矩阵的之字型遍历

描述

给你一个包含 *m* x *n* 个元素的矩阵 (*m* 行, *n* 列), 求该矩阵的之字型遍历。

样例

```
样例 1:
	输入: [[1]]
	输出:  [1]

样例 2:
	输入:   
	[
    [1, 2,  3,  4],
    [5, 6,  7,  8],
    [9,10, 11, 12]
  ]

	输出:  [1, 2, 5, 9, 6, 3, 4, 7, 10, 11, 8, 12]
```

```cpp
class Solution {
public:
    /**
     * @param matrix: An array of integers
     * @return: An array of integers
     */
    vector<int> printZMatrix(vector<vector<int>> &matrix) {
        vector<int>ret;
        if(matrix.empty()||matrix[0].empty()){
            return ret;
        }
        int n=matrix.size(),m=matrix[0].size();
        int i,j;
        for(int s=0;s<=n+m-2;++s){
            if(s%2!=0){
                for(j=min(s,m-1),i=s-j;i<n and i>=0 and j<m and j>=0;++i,--j){
                    ret.push_back(matrix[i][j]);
                }
            }
            else{
                for(i=min(s,n-1),j=s-i;i>=0 and i<n and j>=0 and j<m;--i,++j){
                    ret.push_back(matrix[i][j]);
                }
            }
        }
        return ret;
    }
};
```



# 188. 插入五

给定一个数字，在数字的任意位置插入一个5，使得插入后的这个数字最大

### 样例

**样例 1:**

```
输入:  a = 234
输出: 5234	
```

### 注意事项

|a| \leq 10^6∣*a*∣≤10^6

```cpp
class Solution {
public:
    /**
     * @param a: A number
     * @return: Returns the maximum number after insertion
     */
	int InsertFive(int a) {
		if (a > 0) {
			vector<int>num;
			while (a != 0) {
				num.push_back(a % 10);
				a /= 10;
			}
			size_t numsize = num.size();
			bool add = false;
			for (int i = numsize - 1; i >= 0; --i) {
				if (num[i] < 5) {
					num.insert(num.begin() + i + 1, 5);
					add = true;
					break;
				}
			}
			if (!add) {
				num.push_back(5);
			}
			int sum = 0;
			numsize = num.size();
			for (int i = 0; i < numsize; ++i) {
				sum += num[i] * pow(10, i);
			}
			return sum;
		}
		else if(a<0){
			a = abs(a);
			vector<int>num;
			while (a != 0) {
				num.push_back(a % 10);
				a /= 10;
			}
			size_t numsize = num.size();
			bool add = false;
			for (int i = numsize - 1; i >= 0; --i) {
				if (num[i] > 5) {
					num.insert(num.begin() + i + 1, 5);
					add = true;
					break;
				}
			}
			if (!add) {
				num.push_back(5);
			}
			int sum = 0;
			numsize = num.size();
			for (int i = 0; i < numsize; ++i) {
				sum += num[i] * pow(10, i);
			}
			return -1 * sum;
		}
		else {
			return 50;
		}
	}
};
```

# 309.  交叉数组

描述

给定两个相同长度的数组，通过取第一个数组的第一个元素，第二个数组的第一个元素，第一个数组的第二个元素...依此类推来交叉它们。返回新的交错数组。
注意 ： 长度 ≤ 10000

样例

```
输入: 
[1,2]
[3,4]
输出: 
[1,3,2,4]
```

```cpp
class Solution {
public:
    /**
     * @param A: the array A
     * @param B: the array B
     * @return: returns an alternate array of arrays A and B.
     */
    vector<int> interleavedArray(vector<int> &A, vector<int> &B) {
        vector<int>res;
        if(A.size()==0){
            return res;
        }
        else{
            size_t size= A.size();
            for(int i=0;i<size;i++){
                res.push_back(A[i]);
                res.push_back(B[i]);
            }
        }
        return res;
    }
};
```

# 334. 队列检查

描述

班上的学生根据他们的年级照片的身高升序排列，确定当前未站在正确位置的学生人数

1<= len(heights) <=10^51<=*l**e**n*(*h**e**i**g**h**t**s*)<=1051<= heights[i] <= 10^91<=*h**e**i**g**h**t**s*[*i*]<=109

样例

```
	输入:  heights = [1,1,3,3,4,1]
	输出: 3
	解释:  经过排序后 heights变成了[1,1,1,3,3,4]，有三个学生不在应在的位置上
```

```cpp
bool cmp(int x,int y){
    if(x<y){
        return true;
    }
    else{
        return false;
    }
}
class Solution {
public:
    /**
     * @param heights: Students height
     * @return: How many people are not where they should be
     */
    int orderCheck(vector<int> &heights) {
        int res=0;
        vector<int>count(heights);
        sort(count.begin(),count.end(),cmp);
        for(int i=0;i<count.size();i++){
            if(count[i]!=heights[i]){
                res++;
            }
        }
        return res;
    }
};
```



# 402. 连续子数组求和

给定一个整数数组，请找出一个连续子数组，使得该子数组的和最大。输出答案时，请分别返回第一个数字和最后一个数字的下标。（如果存在多个答案，请返回字典序最小的）

### 样例

**样例 1:**

```
输入: [-3, 1, 3, -3, 4]
输出: [1, 4]
```

**样例 2:**

```
输入: [0, 1, 0, 1]
输出: [0, 3]
解释: 字典序最小.
```

```cpp
class Solution {
public:
    /*
     * @param A: An integer array
     * @return: A list of integers includes the index of the first number and the index of the last number
     */
    vector<int> continuousSubarraySum(vector<int> &A) {
        vector<int>res(2,0);
        int n=A.size();
        int res_sum=A[0];
        int sum=0;
        int l=0;
        for(int r=0;r<n;r++){
            if(sum<0){
                l=r;
                sum=A[r];
            }
            else{
                sum+=A[r];
            }
            if(sum>res_sum){
                res_sum=sum;
                res[0]=l;
                res[1]=r;
            }
        }
        return res;
    }
};
```

# 408. 二进制求和

给定两个二进制字符串，返回他们的和（用二进制表示）。

### 样例

**样例 1：**

```
输入：
a = "0", b = "0"
输出：
"0"
```

**样例 2：**

```
输入：
a = "11", b = "1"
输出：
"100"
```

```cpp
class Solution {
public:
    /**
     * @param a: a number
     * @param b: a number
     * @return: the result
     */
    string addBinary(string &a, string &b) {
		int size=max(a.size(),b.size());
		string res;
		reverse(a.begin(),a.end());
		reverse(b.begin(),b.end());
		int carry=0;
		for(int i=0;i<size;i++){
			int tempa,tempb;
			if(i<a.size()){
				tempa=a[i]-'0';
			}
			else{
				tempa=0;
			}
			if(i<b.size()){
				tempb=b[i]-'0';
			}
			else{
				tempb=0;
			}
			int sum=carry+tempa+tempb;
			carry=0;
			if(sum>=2){
				carry=1;
				sum-=2;
			}
			res.push_back(sum+'0');
		}
		if(carry==1){
			res.push_back('1');
		}
		reverse(res.begin(),res.end());
		return res;
    }
};
```

## 402. 删除链表中的元素

描述

删除链表中等于给定值 `val` 的所有节点。

样例

**样例 1：**

```
输入：head = 1->2->3->3->4->5->3->null, val = 3
输出：1->2->4->5->null
```

**样例 2：**

```
输入：head = 1->1->null, val = 1
输出：null
```

```cpp
/**
 * Definition of singly-linked-list:
 * class ListNode {
 * public:
 *     int val;
 *     ListNode *next;
 *     ListNode(int val) {
 *        this->val = val;
 *        this->next = NULL;
 *     }
 * }
 */

class Solution {
public:
    /**
     * @param head: a ListNode
     * @param val: An integer
     * @return: a ListNode
     */
    ListNode * removeElements(ListNode * head, int val) {
        if(head==NULL){
            return NULL;
        }
        ListNode*befor=NULL;
        ListNode*temp;
        for(temp=head;temp!=NULL;){
            if(temp->val==val){
                if(befor==NULL){
                    head=head->next;
                    if(head==NULL){
                        return NULL;
                    }
                    temp=temp->next;
                }
                else{
                    temp=temp->next;
                }
            }
            else{
                if(befor==NULL){
                    befor=head;
                }
                else{
                    befor->next=temp;
                    befor=temp;
                }
                temp=temp->next;
            }
        }
        befor->next=NULL;
        return head;
    }
};
```

# 551.  嵌套列表的加权和

描述

给一个嵌套的整数列表, 返回列表中所有整数由它们的深度加权后的总和. 每一个元素可能是一个整数或一个列表(其元素也可能是整数或列表)

样例

例1:

```
输入: the list [[1,1],2,[1,1]], 
输出: 10. 
解释:
four 1's at depth 2, one 2 at depth 1, 4 * 1 * 2 + 1 * 2 * 1 = 10
```

例2:

```
输入: the list [1,[4,[6]]], 
输出: 27. 
解释:
one 1 at depth 1, one 4 at depth 2, and one 6 at depth 3; 1 + 4 * 2 + 6 * 3 = 27
```

```cpp
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * class NestedInteger {
 *   public:
 *     // Return true if this NestedInteger holds a single integer,
 *     // rather than a nested list.
 *     bool isInteger() const;
 *
 *     // Return the single integer that this NestedInteger holds,
 *     // if it holds a single integer
 *     // The result is undefined if this NestedInteger holds a nested list
 *     int getInteger() const;
 *
 *     // Return the nested list that this NestedInteger holds,
 *     // if it holds a nested list
 *     // The result is undefined if this NestedInteger holds a single integer
 *     const vector<NestedInteger> &getList() const;
 * };
 */
class Solution {
private:
    int sum=0,depth=1;
public:
    int depthSum(const vector<NestedInteger>& nestedList) {
        for(auto i:nestedList){
            if(i.isInteger()){
                sum+=i.getInteger()*depth;
            }
            else{
                depth++;
                depthSum(i.getList());
                depth--;
            }
        }
        return sum;
    }
};
```

# 987.  具有交替位的二进制数

描述

给一个正整数，检查它的二进制表示是否具有交替位。即，两个相邻的位总是具有不同的值。

样例

**样例 1:**

```
输入: 5
输出: True
解释:
5 的二进制表示为: 101
```

**样例 2:**

```
输入: 7
输出: False
解释:
7 的二进制表示为: 111.
```

**样例 3:**

```
输入: 11
输出: False
解释:
11 的二进制表示为: 1011.
```

**样例 4:**

```
输入: 10
输出: True
解释:
10 的二进制表示: 1010.
```

```cpp
class Solution {
public:
    /**
     * @param n: a postive Integer
     * @return: if two adjacent bits will always have different values
     */
    bool hasAlternatingBits(int n) {
        vector<int>count;
        while(n!=0){
            count.push_back(n%2);
            n/=2;
        }
        if(count[0]==0){
            for(int i=1;1;1){
                if(i<count.size()){
                    if(count[i]==1){
                        i++;
                    }
                    else{
                        return false;
                    }
                }
                else{
                    break;
                }
                if(i<count.size()){
                    if(count[i]==0){
                        i++;
                    }
                    else{
                        return false;
                    }
                }
                else{
                    break;
                }
            }
            return true;
        }
        else{
            for(int i=1;1;1){
                if(i<count.size()){
                    if(count[i]==0){
                        i++;
                    }
                    else{
                        return false;
                    }
                }
                else{
                    break;
                }
                if(i<count.size()){
                    if(count[i]==1){
                        i++;
                    }
                    else{
                        return false;
                    }
                }
                else{
                    break;
                }
            }
            return true;
        }
    }
};
class Solution2 {
public:
    /**
     * @param n: a postive Integer
     * @return: if two adjacent bits will always have different values
     */
    bool hasAlternatingBits(int n) {
        bool sign;
        if(n%2==0){
            sign=true;
            n/=2;
            while(n!=0){
                if(sign==true){
                    if(n%2!=0){
                        n/=2;
                        sign=false;
                    }
                    else{
                        return false;
                    }
                }
                else{
                    if(n%2==0){
                        n/=2;
                        sign=true;
                    }
                    else{
                        return false;
                    }
                }
            }
            return true;
        }
        else{
            sign=false;
            n/=2;
            while(n!=0){
                if(sign==false){
                    if(n%2==0){
                        n/=2;
                        sign=true;
                    }
                    else{
                        return false;
                    }
                }
                else{
                    if(n%2!=0){
                        n/=2;
                        sign=false;
                    }
                    else{
                        return false;
                    }
                }
            }
            return true;
        }
    }
};
```

# 988.  硬币摆放

描述

你有 n 枚硬币，想要摆放成阶梯形状，即第 k 行恰好有 k 枚硬币。

给出 n，找到可以形成的**完整**楼梯行数。

n 是一个非负整数，且在32位有符号整数范围内。

样例

**样例 1:**

```
输入：n = 5
输出：2
解释：
硬币可以形成以下行：
¤
¤ ¤
¤ ¤
因为第3行不完整，我们返回2。
```

**样例 2:**

```
输入：n = 8
输出：3
解释：
硬币可以形成以下行：
¤
¤ ¤
¤ ¤ ¤
¤ ¤
因为第4行不完整，我们返回3。
```

```cpp
class Solution {
public:
    /**
     * @param n: a non-negative integer
     * @return: the total number of full staircase rows that can be formed
     */
    int arrangeCoins(int n) {
        int res=1,sum=0;
        while(1){
            sum+=res;
            if(sum<=n){
                res++;
            }
            else{
                return res-1;
            }
        }
    }
};
```

# 1013. 独特的摩尔斯编码

描述

摩尔斯电码定义了一种标准编码，把每个字母映射到一系列点和短划线，例如：`a` -> `.-`，`b` -> `-...`，`c` ->`-.-.`。

给出26个字母的完整编码表格：

```
[".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]
```

现在给定一个单词列表，每个单词中每个字母可以写成摩尔斯编码。 例如，`cab`可以写成`-.-.-....-`，（把`c`,`a`,`b`的莫尔斯编码串接起来）。 我们称之为一个词的转换。

返回所有单词中不同变换的数量。

`words`的长度最多为`100`.每一个`words[i]`的长度范围为`[1, 12]`.`words[i]`仅仅包含小写字母.

样例

**样例1：**

```
输入: words = ["gin", "zen", "gig", "msg"]
输出: 2
解释: 
每一个单词的变换是:
"gin" -> "--...-."
"zen" -> "--...-."
"gig" -> "--...--."
"msg" -> "--...--."

这里有两种不同的变换结果： "--...-."和"--...--.".
```

**样例2：**

```
输入: words = ["a", "b"]
输出: 2
解释: 
每一个单词的变换是:
"a" -> ".-"
"b" -> "-..."
这里有两种不同的变换结果：".-" and "-...".
```

```cpp
class Solution {
public:
    /**
     * @param words: the given list of words
     * @return: the number of different transformations among all words we have
     */
    int uniqueMorseRepresentations(vector<string> &words) {
        string cnt[]={".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."};
        set<string> coll;
        for(string item:words){
            string tmp;
            for(int i=0;i<item.size();++i){
                tmp+=cnt[item[i]-'a'];
            }
            coll.insert(tmp);
        }
        return coll.size();
    }
};
```

# 1148. 最长和谐子序列

描述

我们将一个和谐数组定义为是其最大值和最小值之间的差值恰好为1的数组。

现在，给定一个整数数组，您需要在其所有可能的子序列中找到其最长的和谐子序列的长度。

输入数组的长度不会超过20,000。

样例

```
输入：[1,3,2,2,5,2,3,7]
输出：5
解释：最长的和谐子序列是[3,2,2,2,3]。
```

```cpp
class Solution {
public:
    /**
     * @param nums: a list of integers
     * @return: return a integer
     */
    int findLHS(vector<int> &nums) {
        map<int,int>count;
        int ans=0;
        for(auto num:nums){
            count[num]++;
        }
        for(auto num:nums){
            if(count[num] and count[num-1]){
                ans=max(ans,count[num]+count[num-1]);
            }
        }
        return ans;
    }
};
```

# 1746. 二叉搜索树结点最小距离

给定一个二叉搜索树的根结点 root, 返回树中任意两节点的差的最小值。

### 样例

**样例 1:**

```
输入: root = {4,2,6,1,3}
输出: 1
解释:
注意，root是树结点对象(TreeNode object)，而不是数组。

给定的树 [4,2,6,1,3,null,null] 可表示为下图:

          4
        /   \
      2      6
     / \    
    1   3  

最小的差值是 1, 它是节点1和节点2的差值, 也是节点3和节点2的差值。
```

**样例 2:**

```
输入: root = {2,1}
输出: 1
解释:
注意，root是树结点对象(TreeNode object)，而不是数组。

给定的树 {2,1} 可表示为下图:

      2
     / 
    1 

最小的差值是 1, 它是节点1和节点2的差值。
```

### 注意事项

-    二叉树的大小范围在 2 到 100。
-    二叉树总是有效的，每个节点的值都是整数，且不重复。

```cpp
/**
 * Definition of TreeNode:
 * class TreeNode {
 * public:
 *     int val;
 *     TreeNode *left, *right;
 *     TreeNode(int val) {
 *         this->val = val;
 *         this->left = this->right = NULL;
 *     }
 * }
 */

class Solution {
public:
    int res=INT_MAX,pre=-1;
    /**
     * @param root:  a Binary Search Tree (BST) with the root node
     * @return: the minimum difference
     */
    int minDiffInBST(TreeNode * root) {
        if(root->left!=NULL){
            minDiffInBST(root->left);
        }
        if(pre>=0){
            res=min(res,root->val-pre);
        }
        pre=root->val;
        if(root->right!=NULL){
            minDiffInBST(root->right);
        }
        return res;
    }
};
```

