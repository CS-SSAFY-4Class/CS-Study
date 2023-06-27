# Radix sort

<br/>

- 기수 정렬(radix sort)은 기수 별로 비교 없이 수행하는 정렬 알고리즘이다. 기수로는 정수, 낱말, 천공카드 등 다양한 자료를 사용할 수 있으나 크기가 유한하고 사전순으로 정렬할 수 있어야 한다. 버킷 정렬의 일종으로 취급되기도 한다.
    - 기수에 따라 원소를 버킷에 집어 넣기 때문에 비교 연산이 불필요하다. 유효숫자가 두 개 이상인 경우 모든 숫자 요소에 대해 수행될 때까지 각 자릿수에 대해 반복한다. 반복할 때마다 기수의 도메인 크기만큼의 누적합이 요구된다.
    - 전체 시간 복잡도는 O(w(n+k)) -> w는 기수의 크기, k는 기수의 도메인 크기가 된다.
    - 정수와 같은 자료의 정렬 속도가 매우 빠르다. 하지만, 데이터 전체 크기에 기수 테이블의 크기만한 메모리가 더 필요하다. 기수 정렬은 정렬 방법의 특수성 때문에, 부동소수점 실수처럼 특수한 비교 연산이 필요한 데이터에는 적용할 수 없지만, 사용 가능할 때에는 매우 좋은 알고리즘이다.

<br/>

- **기수정렬의 역사**
  - 기수 정렬의 역사는 1887년 허먼 홀러리스가 작표기를 만들 때까지 거슬러 올라간다. 기수 정렬 알고리즘은 이미 1923년에 천공 카드를 분류하는 방법으로 널리 사용되었다.
  - Harold H. Seward은 1954년 매사추세츠 공과대학교에서 최초로 메모리 효율적인 컴퓨터 알고리즘을 개발했다. 이전까지는 알 수 없는 크기의 버킷을 가변 할당해야 한다고 믿었기 때문에 전산화 된 기수 정렬은 비현실적인 것으로 생각되었다. Seward의 혁신은 선형 탐색으로 사용하여 필요한 버킷 크기와 오프셋을 미리 결정하여 보조 메모리에서 단일 정적 할당만 할 수 있도록 하는 것이다. 이 선형 탐색은 Seward의 다른 알고리즘인 계수 정렬과 밀접한 관련이 있다.
  - 현대에는 이진 문자열과 정수 정렬에 가장 널리 적용된다. 일부 벤치마크에서 다른 범용 정렬 알고리즘보다 50%에서 3배까지 빠를 때도 있는 것으로 나타났다.

<br/>

- **시간 복잡도**

<br/>

![image](https://wikimedia.org/api/rest_v1/media/math/render/svg/b41c62299c7adb9c929ab0d52b004898441eee2c)  

- **알고리즘**
  1. MSD 기수 정렬은 문자열이나 고정 길이 정수 표현 정렬에 적합하다. [b, c, e, d, f, g, ba]는 [b, ba, c, d, e, f, g] 로 정렬된다. 
      - 특이한 점이 있다면 MSD 정렬은 불안정 정렬이므로 중복 키의 원래 순서를 항상 유지하지는 않는다.
  2. 사전식 순서로 10진법의 가변 길이 정수를 정렬하면 1부터 10까지의 숫자는 [1, 10, 2, 3, 4, 5, 6, 7, 8, 9] 로 출력된다. 더 짧은 키는 왼쪽 정렬되고 오른쪽이 공백 문자로 채워지는 셈이다.


<br/>


### 진행 과정

</br>

- Radix sort

![image](https://i.imgur.com/gcVBdYZ.png)

- with Linked list

![image](https://i.imgur.com/0kRMgFx.png)


<br/>

- visaulization
    - https://www.youtube.com/watch?v=LyRWppObda4
- radix_sort dance
    - https://www.youtube.com/watch?v=ibtN8rY7V5k



### 기수정렬 장단점
- 장점 : 문자열, 정수 정렬 가능
- 단점 : 자릿수가 없는 것은 정렬할 수 없음. (부동 소숫점) 중간 결과를 저장할 bucket 공간이 필요함.


<br/>

- python

<br/>

```python
from math import log
def radix_sort(list, base=10):
    # 입력된 리스트 가운데 최대값의 자릿수 확인
    digit = int(log(max(list), base) + 1)
    # 자릿수 별로 counting sort
    for d in range(digit):
        list = counting_sort_with_digit(list, d, base)
    return list
```

<br/>

- java
<br/>

```java
void countSort(int arr[], int n, int exp) {
	int buffer[n];
    int i, count[10] = {0};
    
    // exp의 자릿수에 해당하는 count 증가
    for (i = 0; i < n; i++){
        count[(arr[i] / exp) % 10]++;
    }
    // 누적합 구하기
    for (i = 1; i < 10; i++) {
        count[i] += count[i - 1];
    }
    // 일반적인 Counting sort 과정
    for (i = n - 1; i >= 0; i--) {
        buffer[count[(arr[i]/exp) % 10] - 1] = arr[i];
        count[(arr[i] / exp) % 10]--;
    }
    for (i = 0; i < n; i++){
        arr[i] = buffer[i];
    }
}

void radixsort(int arr[], int n) {
     // 최댓값 자리만큼 돌기
    int m = getMax(arr, n);
    
    // 최댓값을 나눴을 때, 0이 나오면 모든 숫자가 exp의 아래
    for (int exp = 1; m / exp > 0; exp *= 10) {
        countSort(arr, n, exp);
    }
}
int main() {
    int arr[] = {170, 45, 75, 90, 802, 24, 2, 66};
    int n = sizeof(arr) / sizeof(arr[0]);			// 좋은 습관
    radixsort(arr, n);
    
    for (int i = 0; i < n; i++){
        cout << arr[i] << " ";
    }
    return 0;
}
```
<br/>

- c
```c
void rxSort(int *data, int size, int p, int k) {
    int *counts, // 특정 자리에서 숫자들의 카운트
        *temp; // 정렬된 배열을 담을 임시 장소
    int index, pval, i, j, n;
    // 메모리 할당
    if ( (counts = (int*) malloc(k * sizeof(int))) == NULL )
      return;
    if ( (temp = (int*) malloc(size * sizeof(int))) == NULL )
      return;
    for (n=0; n<p; n++) { // 1의 자리, 10의자리, 100의 자리 순으로 진행
      for (i=0; i<k; i++)
        counts[i] = 0; // 초기화
       // 위치값 계산.
      // n:0 => 1,  1 => 10, 2 => 100
      pval = (int)pow((double)k, (double)n);
      // 각 숫자의 발생횟수를 센다.
      for (j=0; j<size; j++) {
        // 253이라는 숫자라면
        // n:0 => 3,  1 => 5, 2 => 2
        index = (int)(data[j] / pval) % k;
        counts[index] = counts[index] + 1;
      }
      // 카운트 누적합을 구한다. 계수정렬을 위해서.
      for (i=1; i<k; i++) {
        counts[i] = counts[i] + counts[i-1];
      }
      // 카운트를 사용해 각 항목의 위치를 결정한다.
      // 계수정렬 방식
      for (j=size-1; j>=0; j--) { // 뒤에서부터 시작
        index = (int)(data[j] / pval) % k;
        temp[counts[index] -1] = data[j];
        counts[index] = counts[index] - 1; // 해당 숫자 카운트를 1 감소
      }
      // 임시 데이터 복사
      memcpy(data, temp, size * sizeof(int));
    }
    free(counts);
    free(temp);
```




### 참고
<br/>

- 위키피디아 
  - https://ko.wikipedia.org/wiki/%EA%B8%B0%EC%88%98_%EC%A0%95%EB%A0%AC
- github 
  - https://github.com/gyoogle/tech-interview-for-developer
  - https://ratsgo.github.io/
- youtube
- tistory
    - https://wonjayk.tistory.com/
    - https://seanpark11.tistory.com/
