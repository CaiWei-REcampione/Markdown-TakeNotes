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

