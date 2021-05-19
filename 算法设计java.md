# 排序

## 冒泡排序

```java
import java.util.List;
import java.util.ArrayList;
import java.util.Random;

public class SortList {

    private List list;

    boolean hasSort;

    public SortList(int _size){

        list=new ArrayList();
        initialElem(_size);
    }

    private void initialElem(int _size) {

        hasSort=false;
        Random random = new Random();

        for (int i = 0; i < _size; ++i) {

            list.add(random.nextInt(1000));
        }
    }

    public void bubbleSort() {

        for (int i = 0; i < list.size(); i++) {

            for(int j=0;j<list.size()-i-1;++j){

                if((int)list.get(j)<(int)list.get(j+1)){

                    int tmp=(int)list.get(j);
                    list.set(j,list.get(j+1));
                    list.set(j+1,tmp);
                }
            }
        }

        hasSort=true;
    }

    public void printElem() {

        if(!hasSort){
            System.out.println("before sort:");
        }else{
            System.out.println("after sort:");
        }

        for (Object item : list) {

            int value = (int) item;
            System.out.printf("%d ", value);
        }
        System.out.println();
    }
}
```

## 插入排序

```java
import java.util.List;
import java.util.ArrayList;
import java.util.Random;

public class InsertionList {

    private List list;

    private boolean hasSort;

    public InsertionList(int _size){

        list=new ArrayList();
        initialList(_size);
    }

    private void initialList(int _size){

        hasSort=false;

        Random random=new Random();

        for(int i=0;i<_size;++i){

            list.add(random.nextInt(1000));
        }
    }

    public void insertSort(){

        hasSort=true;

        for(int i=1;i<list.size();++i){

            int tmp=(int)list.get(i);

            int j;
            for(j=i-1;j>=0 && (int)list.get(j)>tmp;--j){

                list.set(j+1,list.get(j));
            }
            list.set(j+1,tmp);
        }
    }

    public void showList(){

        if(!hasSort){
            System.out.println("before sort:");
        }else{
            System.out.println("after sort:");
        }

        for(Object item:list) {

            int value=(int)item;
            System.out.printf(value+" ");
        }
        System.out.println();
    }
}
```

## 选择排序

```java
import java.util.List;
import java.util.ArrayList;
import java.util.Random;

public class SelecteList {

    private List list;

    private boolean hasSort;

    public SelecteList(int _size) {

        list = new ArrayList();
        initialList(_size);
    }

    private void initialList(int _size) {

        hasSort = false;

        Random random = new Random();

        for (int i = 0; i < _size; ++i) {

            list.add(random.nextInt(1000));
        }
    }

    public void sortList() {

        hasSort = true;

        for (int i = 0; i < list.size(); ++i) {

            int maxindex = i;
            for (int j = i + 1; j < list.size(); ++j) {

                if ((int) list.get(maxindex) < (int) list.get(j)) {

                    maxindex = j;
                }
            }
            int tmp = (int) list.get(i);
            list.set(i, list.get(maxindex));
            list.set(maxindex, tmp);
        }
    }

    public void showList() {

        if (!hasSort) {
            System.out.println("before sort");
        } else {
            System.out.println("after sort");
        }

        for (Object item : list) {

            int value = (int) item;
            System.out.printf(value + " ");
        }
        System.out.println();
    }
}
```

## 快速排序

```cpp
import java.util.List;
import java.util.ArrayList;
import java.util.Random;

public class SortList {

    private List list;

    private boolean hasSort;

    public SortList(int _size) {

        list = new ArrayList();
        initialList(_size);
    }

    private void initialList(int _size) {

        hasSort = false;

        Random random = new Random();

        for (int i = 0; i < _size; ++i) {

            list.add(random.nextInt(1000));
        }
    }

    public void quickSort(int _left,int _right){

        int tleft=_left;
        int tright=_right;
        int middle=(int)list.get((tleft+tright)/2);
        while(tleft<=tright){

            while((int)list.get(tleft)<middle){

                ++tleft;
            }
            while(middle<(int)list.get(tright)){

                --tright;
            }
            if(tleft<=tright){

                int tmp=(int)list.get(tleft);
                list.set(tleft,list.get(tright));
                list.set(tright,tmp);
                ++tleft;
                --tright;
            }
        }
        if(tleft==tright){

            ++tleft;
        }
        if(_left<tright){

            quickSort(_left,tleft-1);
        }
        if(tleft<_right){

            quickSort(tright+1,_right);
        }
    }

    public void showList() {

        if (!hasSort) {
            System.out.println("before sort");
        } else {
            System.out.println("after sort");
        }

        for (Object item : list) {

            int value=(int)item;
            System.out.printf(value+" ");
        }
        System.out.println();
    }
}
```

# 大小写转换

```java
import java.awt.*;

public class Case {

    private char lowCase;

    private char upperCase;

    public Case(char _lowCase) {

        if (checklowCase(_lowCase)) {

            lowCase = _lowCase;
            upperCase = (char) (lowCase - 'a' + 'A');
        } else {

            System.out.println("error!");
        }
    }

    public char getLowCase() {

        return lowCase;
    }

    public char getUpperCase() {

        return upperCase;
    }

    private boolean checklowCase(char _lowCase) {

        return _lowCase >= 'a' && _lowCase <= 'z';
    }
}
```

# Fibonacci数列

```java
import java.util.Vector;

public class Fibonacci {

    private Vector<Long> cnt;

    public Fibonacci(int maxsize) {

        cnt = new Vector<>();
        cnt.setSize(maxsize);
        Count();
    }

    private void Count() {

        cnt.set(0, (long) 1);
        cnt.set(1, (long) 1);

        for (int i = 2; i < cnt.size(); ++i) {

            cnt.set(i, (long) (cnt.get(i - 1) + cnt.get(i - 2)));
        }
    }

    public long get(int index) {

        return cnt.get(index);
    }
}
```

# 阶乘

```java
public class Factorial {

    private long value[];

    public Factorial(int _num) {

        value = new long[_num];
        value[0] = 1;
        for (int i = 1; i < _num; ++i) {

            value[i] = value[i - 1] * (i+1);
        }
    }
}
```

# 最小公倍数和最大公因数

```java
public class Number {

    private long valueX;
    private long valueY;

    private long leastCommon;// 最大公因数
    private long commonMultiple;// 最小公倍数

    public Number(long _valueX, long _valueY) {

        valueX = _valueX;
        valueY = _valueY;
        count();
    }

    private void count() {

        long tmpX = valueX;
        long tmpY = valueY;
        long r;

        do {
            r = tmpX % tmpY;
            tmpX = tmpY;
            tmpY = r;
        } while (r > 0);

        leastCommon = (valueX * valueY) / tmpX;
        commonMultiple = tmpX;
    }

    public long getLeastCommon(){

        return leastCommon;
    }

    public long getCommonMultiple(){

        return commonMultiple;
    }
}
```

# 水仙花数

```java
import java.util.Vector;

public class NarcissisticNumber {

    private Vector<Integer>cnt;// 水仙花数

    public NarcissisticNumber(){

        cnt=new Vector<>();
        for(int i=100;i<1000;++i){

            int tmpi=i;
            int sum=0;
            while(tmpi!=0){

                sum+=Math.pow(tmpi%10,3);
                tmpi/=10;
            }

            if(sum==i){

                cnt.add(sum);
            }
        }
    }

    public Vector<Integer> getNarcissisticNumber(){

        return cnt;
    }
}
```

# 判断质数

```java
public class Prime {

    private long value;

    public Prime(long _value) {

        value = _value;
    }

    public boolean circulationMethod() {

        for (int i = 2; i <= Math.sqrt(value); ++i) {

            if (value % i == 0) {

                return false;
            }
        }
        return true;
    }
}
```

# 交换数值

```java
public class Number {

    private int x;
    private int y;

    public Number(int x,int y){

        this.x=x;
        this.y=y;
    }

    public void swap(){

        int tmp=x;
        x=y;
        y=tmp;
    }

    public int getX(){

        return x;
    }

    public int getY(){

        return y;
    }
}
```

# 排列数

```java
public class Number {

    public void nextPermutation(int[] nums) {
        int i = nums.length-2;
        while (i>=0 && nums[i+1] <=nums[i]){
            i--;
        }
        if (i >=0){
            int j = nums.length -1;
            while (j>=0 && nums[j] <= nums[i]){
                j--;
            }
            swap(nums,i,j);
        }
        reverse(nums,i+1);
    }

    private void reverse(int[] nums, int start) {
        int i = start,j = nums.length -1;
        while (i < j){
            swap(nums,i,j);
            i++;
            j--;
        }
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

