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

### 插入排序	insertionSort

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

### 快速排序	quickSort

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
	while (tleft < tright) {
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

>    简便方法
>
>    使用<algorithm>头文件的sort函数
>
>    sort(object.begin(),object.end(),less<>())//从小到大
>
>    sort(object.begin(),object.end(),greater<>())//从大到小

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
```

# 计数

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

