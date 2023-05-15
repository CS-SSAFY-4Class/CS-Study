# Merge Sort (병합 정렬)

<br/>

- 합병 정렬 또는 병합 정렬(merge sort)은 O(n log n) 비교 기반 정렬 알고리즘이다.
    - 일반적인 방법으로 구현했을 때 이 정렬은 안정 정렬에 속하며, 분할 정복 알고리즘의 하나이다.
    - 존 폰 노이만이 1945년에 개발했다. 상향식 합병 정렬에 대한 자세한 설명과 분석은 1948년 초 헤르만 골드스타인과 폰 노이만의 보고서에 등장하였다.

    <br/>


### 정렬되는 순서 (두가지 방법이 존재)

<br/>

  - n-way 합병 정렬

      1. 정렬되지 않은 리스트를 각각 하나의 원소만 포함하는 n개의 부분리스트로 분할한다.
      2. 부분리스트가 하나만 남을 때까지 반복해서 병합하며 정렬된 부분리스트를 생성한다. 
      3. 마지막 남은 부분리스트가 정렬된 리스트이다.
  - 하향식 2-way 합병 정렬
      1. 리스트의 길이가 1 이하이면 이미 정렬된 것으로 본다. 
      2. 분할(divide): 정렬되지 않은 리스트를 절반으로 잘라 비슷한 크기의 두 부분 리스트로 나눈다.
      3. 정복(conquer): 각 부분 리스트를 재귀적으로 합병 정렬을 이용해 정렬한다.
      4. 결합(combine): 두 부분 리스트를 다시 하나의 정렬된 리스트로 합병한다. 이때 정렬 결과가 임시배열에 저장된다.
      5. 복사(copy): 임시 배열에 저장된 결과를 원래 배열에 복사한다.

<br/>

![image](https://gmlwjd9405.github.io/images/algorithm-merge-sort/merge-sort-concepts.png)

<br/>

### 시간 복잡도

<br/>

```python

T(n)  =  0 (if n=1)

      =  T(n/2) + T(n/2) + n​ (otherwise)

```

<br/>

최악 시간 복잡도 : O(n log n) <br/>

최선 시간 복잡도 : O(n log n)<br/>

평균 시간 복잡도 : O(n log n)<br/>


<br/>

![image](https://gmlwjd9405.github.io/images/algorithm-merge-sort/sort-time-complexity-etc.png)

<br/>



### 진행 과정

</br>

![image](https://gmlwjd9405.github.io/images/algorithm-merge-sort/merge-sort.png)


<br/>


- visaulization
    - https://www.youtube.com/watch?v=ZRPoEKHXTJg
- mergesort dance
    - https://www.youtube.com/watch?v=dENca26N6V4

<br/>

### 머지 정렬 코드

<br/>

- python

<br/>

```python
def merge_sort(arr):
    if len(arr) < 2:
        return arr

    mid = len(arr) // 2
    low_arr = merge_sort(arr[:mid])
    high_arr = merge_sort(arr[mid:])

    merged_arr = []
    l = h = 0
    while l < len(low_arr) and h < len(high_arr):
        if low_arr[l] < high_arr[h]:
            merged_arr.append(low_arr[l])
            l += 1
        else:
            merged_arr.append(high_arr[h])
            h += 1
    merged_arr += low_arr[l:]
    merged_arr += high_arr[h:]
    return merged_arr
```

<br/>

- python one more

```python
def merge_sort(numbers):
    if len(numbers) == 1:
        return numbers
    mid = len(numbers)//2
    left_numbers = merge_sort(numbers[:mid])
    right_numbers = merge_sort(numbers[mid:])
    left_idx = right_idx = k = 0
    while left_idx < len(left_numbers) and right_idx < len(right_numbers):
        if left_numbers[left_idx] < right_numbers[right_idx]:
            numbers[k] = left_numbers[left_idx]
            left_idx += 1
        else:
            numbers[k] = right_numbers[right_idx]
            right_idx += 1
        k += 1

    if left_idx < len(left_numbers):
        numbers[k:] = left_numbers[left_idx:]
    if right_idx < len(right_numbers):
        numbers[k:] = right_numbers[right_idx:]

    return numbers


```

- java

<br/>

```java
public class MergeSorter {
    public static int[] sort(int[] arr) {
        if (arr.length < 2) return arr;

        int mid = arr.length / 2;
        int[] low_arr = sort(Arrays.copyOfRange(arr, 0, mid));
        int[] high_arr = sort(Arrays.copyOfRange(arr, mid, arr.length));

        int[] mergedArr = new int[arr.length];
        int m = 0, l = 0, h = 0;
        while (l < low_arr.length && h < high_arr.length) {
            if (low_arr[l] < high_arr[h])
                mergedArr[m++] = low_arr[l++];
            else
                mergedArr[m++] = high_arr[h++];
        }
        while (l < low_arr.length) {
            mergedArr[m++] = low_arr[l++];
        }
        while (h < high_arr.length) {
            mergedArr[m++] = high_arr[h++];
        }
        return mergedArr;
    }
}
```
<br/>

- c
  - 톱 다운 구현

  <br/>

```c
/// merge sort range : [low ~ high]
void mergeSort(int A[], int low, int high, int B[]){
    // 1. base condition
    if(low >= high) return;

    // 2. divide
    int mid = (low + high) / 2;

    // 3. conquer
    mergeSort(A, low, mid, B);
    mergeSort(A, mid+1, high, B);

    // 4. combine
    int i=low, j=mid+1, k=low;
    for(;k<=high;++k){
        if(j > high ) B[k] = A[i++];
        else if(i > mid) B[k] = A[j++];
        else if(A[i] <= A[j]) B[k] = A[i++];
        else B[k] = A[j++];
    }

    // 5. copy
    for(i=low;i<=high;++i) A[i] = B[i];
}
```

<br/>

  - 바텀 업 구현

<br/>

```c
// array A[] has the items to sort; array B[] is a work array
void BottomUpMergeSort(A[], B[], n)
{
    // Each 1-element run in A is already "sorted".
    // Make successively longer sorted runs of length 2, 4, 8, 16... until whole array is sorted.
    for (width = 1; width < n; width = 2 * width)
    {
        // Array A is full of runs of length width.
        for (i = 0; i < n; i = i + 2 * width)
        {
            // Merge two runs: A[i:i+width-1] and A[i+width:i+2*width-1] to B[]
            // or copy A[i:n-1] to B[] ( if(i+width >= n) )
            BottomUpMerge(A, i, min(i+width, n), min(i+2*width, n), B);
        }
        // Now work array B is full of runs of length 2*width.
        // Copy array B to array A for next iteration.
        // A more efficient implementation would swap the roles of A and B.
        CopyArray(B, A, n);
        // Now array A is full of runs of length 2*width.
    }
}

//  Left run is A[iLeft :iRight-1].
// Right run is A[iRight:iEnd-1  ].
void BottomUpMerge(A[], iLeft, iRight, iEnd, B[])
{
    i = iLeft, j = iRight;
    // While there are elements in the left or right runs...
    for (k = iLeft; k < iEnd; k++) {
        // If left run head exists and is <= existing right run head.
        if (i < iRight && (j >= iEnd || A[i] <= A[j])) {
            B[k] = A[i];
            i = i + 1;
        } else {
            B[k] = A[j];
            j = j + 1;
        }
    }
}

void CopyArray(B[], A[], n)
{
    for(i = 0; i < n; i++)
        A[i] = B[i];
}
```



### 참고

<br/>

- 위키피디아 
  - https://ko.wikipedia.org/wiki/%ED%95%A9%EB%B3%91_%EC%A0%95%EB%A0%AC
- github 
  - https://gmlwjd9405.github.io/
  - https://github.com/gyoogle/tech-interview-for-developer
- youtube
- blog
    - https://blog.naver.com/dev_seung2/221608092034
