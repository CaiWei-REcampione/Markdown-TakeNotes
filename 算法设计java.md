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

