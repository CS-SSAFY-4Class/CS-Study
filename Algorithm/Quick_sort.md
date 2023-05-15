# Quick Sort (퀵 정렬)

<br/>

- 퀵 정렬(Quicksort)은 찰스 앤터니 리처드 호어가 개발한 정렬 알고리즘이다.
    - 다른 원소와의 비교만으로 정렬을 수행하는 비교 정렬에 속한다.
    - 원소들 중에 같은 값이 있는 경우 같은 값들의 정렬 이후 순서가 초기 순서와 달라질 수 있어 불안정 정렬에 속한다.

### 정렬되는 순서
  - 퀵 정렬은 분할 정복(divide and conquer) 방법을 통해 리스트를 정렬한다.
      1. 리스트 가운데서 하나의 원소를 고른다. 이렇게 고른 원소를 피벗이라고 한다.
      2. 피벗 앞에는 피벗보다 값이 작은 모든 원소들이 오고, 피벗 뒤에는 피벗보다 값이 큰 모든 원소들이 오도록 피벗을 기준으로 리스트를 둘로 나눈다. 이렇게 리스트를 둘로 나누는 것을 분할이라고 한다. 분할을 마친 뒤에 피벗은 더 이상 움직이지 않는다.
      3. 분할된 두 개의 작은 리스트에 대해 재귀(Recursion)적으로 이 과정을 반복한다. 재귀는 리스트의 크기가 0이나 1이 될 때까지 반복된다.  

- 피벗 선택
    - 퀵 정렬에서 피벗 위치를 결정하는 방법에는 여러 가지 방법이 있다. 기초적인 방법으로는 난수 분할이 사용되는데 안정성이 떨어진다.
        - 일반적으로는 좌측 끝, 중앙, 우측 끝 등의 중위법을 이용하여 분할한다.

![image](https://upload.wikimedia.org/wikipedia/commons/thumb/8/84/Partition_example.svg/200px-Partition_example.svg.png)

<br/>

### 시간 복잡도

<br/>
최악 시간 복잡도 : O(n2) <br/>
최선 시간 복잡도 : O(n log n)<br/>
평균 시간 복잡도 : O(n log n)<br/>


![image](https://wikimedia.org/api/rest_v1/media/math/render/svg/56572f92a7140a67a4dad085c0e71392eb98a2be)

<br/>




### 진행 과정

</br>

![image](https://upload.wikimedia.org/wikipedia/commons/thumb/a/af/Quicksort-diagram.svg/200px-Quicksort-diagram.svg.png)


<br/>

fivot 기준으로 계속 정렬된다. 밑부분 코드를 보면 재귀가 돌아가며 정렬되는 것을 확인할 수 있다.
```
left, equal, right가 fivot 기준으로 정렬해서 합쳐진다.
list_num = [1, 3, 2, 5, 7, 6, 8, 0, 9, 4]

1. [1, 3, 2, 5, 0, 4] [6] [7, 8, 9] -> 6을 기준으로 나눈다.
2. [1, 3, 2, 0, 4] [5] [] -> 6 보다 작은 수들 중 5를 기준으로 나눈다.
3. [1, 0] [2] [3, 4] -> 5보다 작은 수들에서 2 기준으로 정렬한다. 
4. [] [0] [1] -> 남은 수들을 정렬한다.
5. [3] [4] [] -> 3번에서 fivot 오른쪽 부분을 정렬한다. 
6. [7] [8] [9] -> 2번에서 오른쪽 부분을 정렬한다.
7. [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] -> 완성


```

- visaulization
    - https://www.youtube.com/watch?v=8hEyhs3OV1w
- selection dance
    - https://www.youtube.com/watch?v=3San3uKKHgg



### 퀵 정렬 코드
- python
<br/>

```python
def quicksort(x):
    if len(x) <= 1:
        return x

    pivot = x[len(x) // 2]
    less = []
    more = []
    equal = []
    for a in x:
        if a < pivot:
            less.append(a)
        elif a > pivot:
            more.append(a)
        else:
            equal.append(a)

    return quicksort(less) + equal + quicksort(more)
```

<br/>

- java
<br/>

```java
public void quickSort(int[] arr, int left, int right) {
    // base condition
    if (left >= right) {
        return;
    }
    int pivot = arr[right];
    
    int sortedIndex = left;
    for (int i = left; i < right; i++) {
        if (arr[i] <= pivot) {
            swap(arr, i, sortedIndex);
            sortedIndex++;
        }
    }
    swap(arr, sortedIndex, right);
    quickSort(arr, left, sortedIndex - 1);
    quickSort(arr, sortedIndex + 1, right);
}

private void swap(int[] arr, int i, int j) {
    int tmp = arr[i];
    arr[i] = arr[j];
    arr[j] = tmp;
}
```
<br/>

- c
```c
void quickSort(int arr[], int left, int right) {
      int i = left, j = right;
      int pivot = arr[(left + right) / 2];
      int temp;
	  
      while (i <= j)
      {
        while (arr[i] < pivot)	i++; // arr[i] ≥ pivot 일 때까지, left에서 오른쪽 방향으로 탐색
        while (arr[j] > pivot)	j--; // arr[j] ≤ pivot 일 때까지, right에서 왼쪽 방향으로 탐색
		
        if (i <= j) // 큰 값이 작은 값보다 왼쪽에 있으면
        {
			// SWAP(arr[i], arr[j])
            temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
			
            i++;
            j--;
        }
      } 

    /* 재귀(recursion) */
    if (left < j)	quickSort(arr, left, j);
    if (i < right)	quickSort(arr, i, right);
```

- C++
```c++
#include <algorithm>//swap

void quickSort(int A[], int low, int high) {
    if(low >= high) return; // base condition

    // divide process
    int i = low, j = low;
    int&pivot = A[high];
    for (; j < high; ++j) {
        if ( A[j] < pivot)
            swap(A[i++], A[j]);
    }
    swap(A[i], pivot);

    // conquer process
    quickSort(A, low, i-1);
    quickSort(A, i+1, high);
}
```



### 참고
<br/>

- 위키피디아 
  - https://ko.wikipedia.org/wiki/%ED%80%B5_%EC%A0%95%EB%A0%AC
- github 
  - https://gmlwjd9405.github.io/
  - https://github.com/gyoogle/tech-interview-for-developer
- youtube
- blog
    - https://blog.naver.com/dev_seung2/221617833170
