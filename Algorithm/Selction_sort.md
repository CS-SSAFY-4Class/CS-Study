# Selection Sort (선택정렬)

<br/>

- 선택 정렬(selection sort)은 제자리 정렬 알고리즘의 하나이다
    - 정렬되는 순서(오름차순일때)
        1. 주어진 리스트 중 **최소값**을 찾는다.
        2. 그 값을 맨 앞에 위치한 값과 교체한다.
        3. 맨 처음 위치를 뺀 나머지 리스트를 같은 방법으로 교체한다.
        <br/>

- **시간 복잡도**
<br/>

![image](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6bbfd950-b58b-46c8-9aad-8cac8a7bf794/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230314T023116Z&X-Amz-Expires=86400&X-Amz-Signature=ad9d3034499aaf5a9d96ac1dc74675bd40d75b48809b3b67b6a567e39c2e21ed&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

<br/>

### 다른 정렬 알고리즘과의 비교
<br/>

- **거품 정렬(bubble sort)** : 시간 복잡도 Θ ( n**2 )인 정렬 알고리즘 중에서 선택 정렬은 버블 정렬보다 항상 우수하다.

- **삽입 정렬(insertion sort)** : 삽입 정렬은 첫번째 요소가 정렬된 순서로 온다는 점에서 선택정렬과 유사하다. 하지만 삽입 정렬은 필요한 만큼의 요소만 탐색하기 때문에 훨씬 효율적으로 실행된다는 차이가 있다.

- **합병 정렬(merge sort)** : 선택 정렬은 작은 배열에서 더 빠르다. 따라서 충분히 작은 하위 목록에만 삽입 정렬 혹은 선택 정렬을 이용해서 최적화하는 것이 좋다.
<br/>


### 선택 정렬 개선 방법
<br/>

1. **이중 선택 정렬** : 탐색 횟수가 절반으로 줄어들게 된다.

2. **탐색**을 응용하여 개선: 한 번의 탐색 때 동일한 값이 있다면 함께 정렬하는 방법이다. 같은 값이 많을수록 유용하다.
<br/>

### 진행 과정

![image](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/eb9e32f4-870b-4048-9348-e0d295c24e58/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230314T030758Z&X-Amz-Expires=86400&X-Amz-Signature=6d86bebcb681f0db27c1032caf9981980761c8a9634b0fc346ea04f027f5860f&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

<br/>

```
1 부터 9까지 차례대로 고정되면서 정렬된다.

[1, 3, 5, 7, 9, 2, 4, 8, 6] -> 1 고정
[1, 2, 5, 7, 9, 3, 4, 8, 6] -> 2 고정
[1, 2, 3, 7, 9, 5, 4, 8, 6] -> 3 고정
[1, 2, 3, 4, 9, 5, 7, 8, 6] -> 4 고정
[1, 2, 3, 4, 5, 9, 7, 8, 6] -> 5 고정
[1, 2, 3, 4, 5, 6, 7, 8, 9] -> 6 고정
[1, 2, 3, 4, 5, 6, 7, 8, 9] -> 7 고정
[1, 2, 3, 4, 5, 6, 7, 8, 9] -> 8 고정
[1, 2, 3, 4, 5, 6, 7, 8, 9] -> 9 고정

```

- visaulization
    - https://www.youtube.com/watch?v=92BfuxHn2XE
- selection dance
    - https://www.youtube.com/watch?v=0-W8OEwLebQ



### 선택 정렬 코드
- python
<br/>

```python
def selectionSort(x):
	length = len(x)
	for i in range(length-1):
	    indexMin = i
		for j in range(i+1, length):
			if x[indexMin] > x[j]:
				indexMin = j
		x[i], x[indexMin] = x[indexMin], x[i]
	return x
```

<br/>

- java
<br/>

```java
void selectionSort(int[] list) {
    int indexMin, temp;

    for (int i = 0; i < list.length - 1; i++) {
        indexMin = i;
        for (int j = i + 1; j < list.length; j++) {
            if (list[j] < list[indexMin]) {
                indexMin = j;
            }
        }
        temp = list[indexMin];
        list[indexMin] = list[i];
        list[i] = temp;
    }
}
```
<br/>

- c
```c
void selectionSort(int *list, const int n)
{
    int i, j, indexMin, temp;

    for (i = 0; i < n - 1; i++)
    {
        indexMin = i;
        for (j = i + 1; j < n; j++)
        {
            if (list[j] < list[indexMin])
            {
                indexMin = j;
            }
        }
        temp = list[indexMin];
        list[indexMin] = list[i];
        list[i] = temp;
    }
}
```







### 참고
<br/>

- 위키피디아 
  - https://ko.wikipedia.org/wiki/%EC%84%A0%ED%83%9D_%EC%A0%95%EB%A0%AC
- github 
  - https://gmlwjd9405.github.io/
- youtube
- tistory
    - https://wonjayk.tistory.com/
