# Counting Sort


<br/>

## Counting Sort (계수 정렬)
- 계수 정렬 또는 카운팅 소트(counting sort)는 컴퓨터 과학에서 정렬 알고리즘의 하나로서, 작은 양의 정수들인 키에 따라 객체를 수집하는 것, 즉 정수 정렬 알고리즘의 하나이다. 



## 동작 방법

- 구별되는 키 값들을 소유하는 객체의 수를 계수하고 출력 시퀀스에 각 키 값의 위치를 결정하기 위한 해당 계수에 전위합을 적용함으로써 동작한다. 실행 시간은 항목의 수, 그리고 최대 키 값과 최소 키 값의 차이에 선형적이므로 키의 다양성이 항목의 수보다 상당히 크지 않은 상황에서 직접 사용하는 데에만 적절하다. 
  - 더 큰 키들을 더 효율적으로 처리할 수 있는 다른 정렬 알고리즘인 기수 정렬의 서브루틴에 종종 사용된다.


<br/>

### 대표적인 사례
- Counting Sort를 대표적으로 활용하는 사례는 26개의 알파벳으로 이루어진 문자열에서 Suffix Array를 얻는 경우인데 이때 Counting Sort를 사용하기 때문에 일반적인 Sort를 사용해서 Suffix Array를 얻때 시간복잡도 보다 빠른 에 Suffix Array를 얻는 것이 가능합니다.

<br/>

### 시간 복잡도

 **O(n+k)**

counting sort의 계산복잡성은 O(n+k)
k가 충분히 작을 경우 O(n)이지만
k 값이 커질 경우 k가 counting sort의 복잡성을 지배하게 됩니다. 

<br/>





### 진행 과정


![image](https://blog.kakaocdn.net/dn/c4eo4p/btqBJfGO4Re/J75Juol23cVgkAN15p7D2K/img.png)
 

<br/>


- Counting Sort

![image](https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https:%2F%2Fblog.kakaocdn.net%2Fdn%2FUYWWJ%2FbtqAcroPz11%2FvOI2bFScOOhIscZkMKXgw1%2Fimg.png)



<br/>

- visualization site
    - https://www.cs.usfca.edu/~galles/visualization/CountingSort.html
- visualization    
    - https://www.youtube.com/watch?v=xFPi5BWI06k



<br/>

## 중요사항
- 카운팅 정렬은 입력 데이터의 범위가 정렬할 개체 수보다 크게 크지 않은 경우에 효율적입니다. 입력 시퀀스가 ​​1~10K 범위에 있고 데이터가 10, 5, 10K, 5K인 상황을 고려하면서 사용해야합니다. 
- 비교 기반 정렬이 아닙니다. 실행 시간 복잡도는 데이터 범위에 비례하는 공간에서 O(n)입니다. 
- 카운팅 정렬은 우리가 정렬하는 데이터에 대해 가정하기 때문에 이를 달성할 수 있습니다.
기수 정렬과 같은 다른 정렬 알고리즘의 하위 루틴으로 자주 사용됩니다. 
- 계수 정렬은 부분 해싱을 사용하여 O(1)에서 데이터 개체의 발생을 계산합니다.
- 카운팅 정렬은 음의 입력에도 작동하도록 확장할 수 있습니다.
- 카운팅 정렬은 안정적인 알고리즘 입니다 . 그러나 약간의 코드 변경으로 안정적으로 만들 수 있습니다.


<br/>




- python

<br/>

```python
# A: input array
# k: maximum value of A
def counting_sort(A, k):
    
    # B: output array
    # init with -1
    B = [-1] * len(A)
    
    # C: counting array
    # init with zeros
    C = [0] * (k + 1)
    
    # count occurences
    for a in A:
        C[a] += 1
    
    # update C
    for i in range(k):
        C[i+1] += C[i]
    
    # update B
    for j in reversed(range(len(A))):
    	B[C[A[j]] - 1] = A[j]
    	C[A[j]] -= 1

    return B
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

- js

```javascript
#include <cstdio>

#define MAX_SIZE 1000
#define MAX_NUM 10000

int main(){
    int N, A[MAX_SIZE+1], B[MAX_SIZE+1], count[MAX_NUM+1], countSum[MAX_NUM+1];
    
    //수열의 길이 N은 MAX_SIZE이하여야합니다.
    scanf("%d", &N);
    
    //count배열을 모두 0으로 초기화
    for(int i = 0; i<= N ; i++)
        count[i] = 0;
    
    //수열 A에 입력되는 수는 MAX_NUM 이하여야합니다.
    for(int i =1 ; i<= N ; i++){
        scanf("%d", &A[i]);
        
        //숫자 등장 횟수 세기
        count[A[i]]++;
    }
    
    //누적합 구성
    countSum[0] = count[0];
    for(int i = 1 ; i<= MAX_NUM ; i++)
        countSum[i] = countSum[i-1]+count[i];
    
    //뒤에서 부터 수열 A 순회한다.
    for(int i = N ; i >= 1; i--){
        B[countSum[A[i]]] = A[i];
        countSum[A[i]]--;
    }
    
    //수열 A를 정렬한 결과인 수열 B를 출력한다.
    for(int i =1 ; i<= N ; i++)
        printf("%d ", B[i]);
}
```

- c
```c
// C Program for counting sort
#include <stdio.h>
#include <string.h>
#define RANGE 255

// The main function that sort the given string arr[] in
// alphabetical order
void countSort(char arr[])
{
    // The output character array that will have sorted arr
    char output[strlen(arr)];

    // Create a count array to store count of individual
    // characters and initialize count array as 0
    int count[RANGE + 1], i;
    memset(count, 0, sizeof(count));

    // Store count of each character
    for (i = 0; arr[i]; ++i)
        ++count[arr[i]];

    // Change count[i] so that count[i] now contains actual
    // position of this character in output array
    for (i = 1; i <= RANGE; ++i)
        count[i] += count[i - 1];

    // Build the output character array
    for (i = 0; arr[i]; ++i) {
        output[count[arr[i]] - 1] = arr[i];
        --count[arr[i]];
    }

    /*
     For Stable algorithm
     for (i = sizeof(arr)-1; i>=0; --i)
    {
        output[count[arr[i]]-1] = arr[i];
        --count[arr[i]];
    }

    For Logic : See implementation
    */

    // Copy the output array to arr, so that arr now
    // contains sorted characters
    for (i = 0; arr[i]; ++i)
        arr[i] = output[i];
}

```




### 참고
<br/>

- 위키피디아 
  - https://ko.wikipedia.org/wiki/%EA%B3%84%EC%88%98_%EC%A0%95%EB%A0%AC
- github 
  - https://ratsgo.github.io/
- youtube
- tistory
    - https://wonjayk.tistory.com/
    - https://bowbowbow.tistory.com/
- https://www.geeksforgeeks.org/
