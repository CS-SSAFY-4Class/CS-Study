# Selection Sort (선택정렬)

<br/>

- 삽입 정렬(Insertion Sort)는 자료 배열의 모든 요소를 앞에서부터 차례대로 이미 정렬된 배열 부분과 비교하여 자신의 위치를 찾아 삽입함으로 정렬을 완성하는 알고리즘이다.
<br/>

- **시간 복잡도**
  - ![image](https://wikimedia.org/api/rest_v1/media/math/render/svg/6fd040d16ddcc273c6928e0e06485727f2c3c2cf)
  - ![시간복잡도](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392)
<br/>

- 정렬되는 순서

  - 각 반복되는 구간에서 정렬되지 않은 나머지 부분 중 첫 번째 항목은 제거되어서 정확한 위치에 삽입된다.

<br/>

![image](https://upload.wikimedia.org/wikipedia/commons/3/32/Insertionsort-before.png)
![image](https://upload.wikimedia.org/wikipedia/commons/d/d9/Insertionsort-after.png)

<br/>

### 다른 정렬 알고리즘과의 비교
<br/>

- **거품 정렬(bubble sort)** : 거품 정렬과 같은 시간 복잡도 Θ ( n**2 )인 알고리즘에 비교하여 빠르며, 안정적인 정렬이다.

- **선택 정렬(Selection sort)** : 선택 정렬은 첫번째 요소가 정렬된 순서로 온다는 점에서 삽입정렬과 유사하다. 하지만 삽입정렬이 필요 요소만 탐색하기에 조금 더 효율적이다.


<br/>


### 삽입정렬 장단점

<br/>

1. 장점 : 구현이 간단하며 필요 요소만 탐색한다는 장점이 있다.

2. 단점 : 배열이 길어질수록 효율은 떨어질 수 있다.
<br/>

### 진행 과정

</br>

![image](https://upload.wikimedia.org/wikipedia/commons/e/ea/Insertion_sort_001.PNG?20090527211126)


<br/>

```
1 부터 9까지 차례대로 삽입되면서 정렬된다.
예시 arr = [1, 3, 2, 4, 7, 6, 5, 9, 8]

[1, 3, 2, 4, 7, 6, 5, 9, 8] -> 1 삽입
[1, 2, 3, 4, 7, 6, 5, 9, 8] -> 2 삽입
[1, 2, 3, 4, 7, 6, 5, 9, 8] -> 3 삽입
[1, 2, 3, 4, 7, 6, 5, 9, 8] -> 4 삽입
[1, 2, 3, 4, 6, 7, 5, 9, 8] -> 7 이동
[1, 2, 3, 4, 5, 6, 7, 9, 8]-> 5 삽입 
[1, 2, 3, 4, 5, 6, 7, 9, 8] -> 6 삽입
[1, 2, 3, 4, 5, 6, 7, 8, 9]-> 7 삽입
[1, 2, 3, 4, 5, 6, 7, 8, 9] -> 9 삽입 확인!

```

- visaulization
    - https://www.youtube.com/watch?v=8oJS1BMKE64
- selection dance
    - https://www.youtube.com/watch?v=EdIKIf9mHk0



### 선택 정렬 코드
- python
<br/>

```python
def insert_sort(x):
	for i in range(1, len(x)):
		j = i - 1
		key = x[i]
		while x[j] > key and j >= 0:
			x[j+1] = x[j]
			j = j - 1
		x[j+1] = key
	return x
```

<br/>

- java
<br/>

```java
void insertionSort(int[] arr)
{

   for(int index = 1 ; index < arr.length ; index++){

      int temp = arr[index];
      int aux = index - 1;

      while( (aux >= 0) && ( arr[aux] > temp ) ) {

         arr[aux + 1] = arr[aux];
         aux--;
      }
      arr[aux + 1] = temp;
   }
}
```
<br/>

- c
```c
void insertion_sort ( int *data, int n )
{
  int i, j, remember;
  for ( i = 1; i < n; i++ )
  {
    remember = data[(j=i)];
    while ( --j >= 0 && remember < data[j] ){
        data[j+1] = data[j];
    }
    data[j+1] = remember;
  }
}
```

- c++
```c++
#include <iterator>

template<typename biIter>
void insertion_sort(biIter begin, biIter end)
{
    biIter bond = begin;
    for (++bond; bond!=end; ++bond)
    {
      typename std::iterator_traits<biIter>::value_type key = *bond;
      biIter ins = bond;
      biIter pre = ins;
    }
}
```







### 참고
<br/>

- 위키피디아 
  - https://ko.wikipedia.org/wiki/%EC%82%BD%EC%9E%85_%EC%A0%95%EB%A0%AC
- github 
  - https://gmlwjd9405.github.io/
  - https://github.com/gyoogle/tech-interview-for-developer
- youtube
- tistory
    - https://wonjayk.tistory.com/
