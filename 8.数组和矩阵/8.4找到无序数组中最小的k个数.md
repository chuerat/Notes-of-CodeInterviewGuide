> ##### 题目
>
> 给定一个无序的整型数组arr,找到其中最小的k个数。时间复杂度至少为O(Nlogk)。

##### 代码实现

```java
public int[] getMinKNumsByHeap(int[] arr, int k) {
    if (k < 1 || k > arr.length) {
        return arr;
    }

    int[] kHeap = new int[k]; //代表目前被选出的k个最小的数

    for (int i = 0; i != k; i++) {
        heapInsert(kHeap, arr[i], i);
    }
    for (int i = k; i != arr.length; i++) {
        if (arr[i] < kHeap[0]) {
            kHeap[0] = arr[i];
            heapify(kHeap, 0, k);
        }
    }

    return kHeap;
}

//建堆
public void heapInsert(int[] arr, int value, int index) {
    arr[index] = value;
    while (index != 0) {
        int parent = (index - 1) / 2;
        if (arr[parent] < arr[index]) {
            swap(arr, parent, index);
            index = parent;
        } else {
            break;
        }
    }
}

//调整堆
public void heapify(int[] arr, int index, int heapSize) {
    int left = index * 2 + 1;
    int right = index * 2 + 2;
    int largest = index;

    while (left < heapSize) {
        if (arr[left] > arr[index]) {
            largest = left;
        }
        if (right < heapSize && arr[right] > arr[largest]) {
            largest = right;
        }
        if (largest != index) {
            swap(arr, largest, index);
        } else {
            break;
        }

        index = largest;
        left = index * 2 + 1;
        right = right * 2 + 2;
    }
}

public void swap(int[] arr, int index1, int index2) {
    int tmp = arr[index1];
    arr[index1] = arr[index2];
    arr[index2] = tmp;
}
```

