# Heap sort

<br/>

- 힙 정렬(Heap sort)는 최대 힙 트리나 최소 힙 트리를 구성해 정렬을 하는 방법으로서 내림차순 정렬을 위해서 최소 힙을, 오름차순 정렬을 위해서 최대 힙을 구성해서 정렬하는 sorting algorithm이다.
    - 힙 정렬은 1964 J.W.J. 윌리엄스에 위해 발명되었다. 이후 R.W 플로이드가 제자리 정렬을 할 수 있도록 개선하였고 이를 바탕으로 트리 정렬 알고리즘으로 발전할 수 있었다.

    - **알고리즘**
        1. n개의 노드에 대해서 완전 이진 트리를 구성하고 부모노드, 왼쪽 자식 노드, 오른쪽 자식노드 순으로 구성한다.
        2. 최대 힙을 구성하여 단말 노드를 자식 노드로 가진 부모노드부터 구성하며 아래부터 루트까지 올라오며 순차적으로 만들어 갈 수 있다.
        3. 가장 큰 수를 가장 작은 수와 교환한다.
        4. 2와 3을 반복하면서 정렬을 진행한다.

        <br/>

- **시간 복잡도**
<br/>

![image](https://wikimedia.org/api/rest_v1/media/math/render/svg/aae0f22048ba6b7c05dbae17b056bfa16e21807d)  
![image](https://wikimedia.org/api/rest_v1/media/math/render/svg/8efb951070974e8c5c0deff1a64982b45c2108d5)  
![image](https://wikimedia.org/api/rest_v1/media/math/render/svg/4f72efc2c04b53a965a0857eb70ed772bc7e738e)  
![image](https://wikimedia.org/api/rest_v1/media/math/render/svg/499f41baf119336c5451024f119b1f8c4ef2022d)  

- 최소 힙과 최대 힙

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F2665E04E5454788F1C)


<br/>


### 힙을 구현하는 방법
1. 힙을 저장하는 표준적인 자료구조는 배열이다.
2. 구현을 쉽게 하기 위해서 배열의 첫 번째 인덱스인 0은 사용되지 않는다. 
3. 특정 위치의 노드 번호는 새로운 노드가 추가되어도 변하지 않는다.
4. 힙에서 부모와 자식 노드간의 관계
  ```
  왼쪽 자식의 인덱스 = 부모의 인덱스 * 2
  오른쪽 자식의 인덱스 = 부모의 인덱스 * 2 + 1
  부모의 인덱스 = 자식의 인덱스 / 2
  ```

<br/>


![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F2455654F54547CB314)

<br/>


### 다른 정렬 알고리즘과의 비교
<br/>

![image](https://gmlwjd9405.github.io/images/algorithm-heap-sort/sort-time-complexity.png)

- 힙 정렬은 구현하기에는 복잡하지만 효율적인 방법에 속한다.

<br/>


### 진행 과정

</br>

- insert
![image](https://i.imgur.com/PjGdges.png)

- delete
![image](https://i.imgur.com/fPS4LPp.png)


<br/>

```

[7, 2, 5, 3, 4, 6, 1, 9, 8, 0]
[7, 3, 5, 2, 4, 6, 1, 9, 8, 0]
[7, 4, 5, 2, 3, 6, 1, 9, 8, 0]
[7, 4, 6, 2, 3, 5, 1, 9, 8, 0]
[7, 4, 6, 9, 3, 5, 1, 2, 8, 0]
[7, 9, 6, 4, 3, 5, 1, 2, 8, 0]
[9, 7, 6, 4, 3, 5, 1, 2, 8, 0]
[9, 7, 6, 8, 3, 5, 1, 2, 4, 0]
[9, 8, 6, 7, 3, 5, 1, 2, 4, 0]
[8, 0, 6, 7, 3, 5, 1, 2, 4, 9]
[8, 7, 6, 0, 3, 5, 1, 2, 4, 9]
[8, 7, 6, 4, 3, 5, 1, 2, 0, 9]
[7, 0, 6, 4, 3, 5, 1, 2, 8, 9]
[7, 4, 6, 0, 3, 5, 1, 2, 8, 9]
[7, 4, 6, 2, 3, 5, 1, 0, 8, 9]
[6, 4, 0, 2, 3, 5, 1, 7, 8, 9]
[6, 4, 5, 2, 3, 0, 1, 7, 8, 9]
[5, 4, 1, 2, 3, 0, 6, 7, 8, 9]
[4, 0, 1, 2, 3, 5, 6, 7, 8, 9]
[4, 3, 1, 2, 0, 5, 6, 7, 8, 9]
[3, 0, 1, 2, 4, 5, 6, 7, 8, 9]
[3, 2, 1, 0, 4, 5, 6, 7, 8, 9]
[2, 0, 1, 3, 4, 5, 6, 7, 8, 9]
[1, 0, 2, 3, 4, 5, 6, 7, 8, 9]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]


```

- visaulization
    - https://www.youtube.com/watch?v=_bkow6IykGM
- heap_sort dance
    - https://www.youtube.com/watch?v=nms-xZlnHlM



### 힙 정렬 코드
- python
<br/>

```python
arr = [7, 2, 5, 3, 4, 6, 1, 9, 8, 0]

def heap_sort(array):
    n = len(array)
    # heap 구성
    for i in range(n):
        c = i
        while c != 0:
            r = (c-1)//2
            if (array[r] < array[c]):
                array[r], array[c] = array[c], array[r]
            c = r
    # 크기를 줄여가면서 heap 구성
    for j in range(n-1, -1, -1):
        array[0] , array[j] = array[j], array[0]
        r = 0
        c = 1
        while c<j:
            c = 2*r +1
            # 자식 중 더 큰 값 찾기
            if (c<j-1) and (array[c] < array[c+1]):
                c += 1
            # 루트보다 자식이 크다면 교환
            if (c<j) and (array[r] < array[c]):
                array[r], array[c] = array[c], array[r]
            r=c
          
print(heap_sort(arr))
```

<br/>

- java
<br/>

```java
public class Heap
{
	private int[] element; //element[0] contains length
	private static final int ROOTLOC = 1;
	private static final int DEFAULT = 10;

	public Heap(int size) {
		if(size>DEFAULT) {element = new int[size+1]; element[0] = 0;}
		else {element = new int[DEFAULT+1]; element[0] = 0;}
	}

	public void add(int newnum) {

		if(element.length <= element[0] + 1) {
			int[] elementTemp = new int[element[0]*2];
			for(int x = 0; x < element[0]; x++) {
				elementTemp[x] = element[x];
			}
			element = elementTemp;
		}
		element[++element[0]] = newnum;
		upheap();
	}

	public int extractRoot() {
		int extracted = element[1];
		element[1] = element[element[0]--];
		downheap();
		return extracted;
	}

	public void upheap() {
		int locmark = element[0];
		while(locmark > 1 && element[locmark/2] > element[locmark]) {
			swap(locmark/2, locmark);
			locmark /= 2;
		}
	}

	public void downheap() {
		int locmark = 1;
		while(locmark * 2 <= element[0])
		{
			if(locmark * 2 + 1 <= element[0]) {
				int small = smaller(locmark*2, locmark*2+1);
				if(element[small] >= element[locmark]) break;
				swap(locmark,small);
				locmark = small;
			}
			else {
			    if(element[locmark * 2] >= element[locmark]) break;
				swap(locmark, locmark * 2);
				locmark *= 2;
			}
		}
	}

	public void swap(int a, int b) {
		int temp = element[a];
		element[a] = element[b];
		element[b] = temp;
	}

	public int smaller(int a, int b) {
		return element[a] < element[b] ? a : b;
	}
}
```
<br/>

- c
```c
void downheap(int cur, int k)
{
  int left, right, p;
    while(cur < k) {
      left = cur * 2 + 1;
      right = cur * 2 + 2;

      if (left >= k && right >= k) break;

      p = cur;
      if (left < k && data[p] < data[left]) {
        p = left;
      }
      if (right < k && data[p] < data[right]) {
        p = right;
      }
      if (p == cur) break;

      swap(&data[cur],&data[p]);
      cur=p;
    }
}

void heapify(int n)
{
  int i,p;
  for(i = (n-1)/2; i >= 0; i--){
    downheap(i,n);
  }
  //for(i=0;i<size;++i)printf("%d ",data[i]);
  //printf("\n");
}

void heap()
{
  int k;
  heapify(size);
  for(k = size-1; k > 0; ){
    swap(&data[0],&data[k]);
    //k--;
    downheap(0,k);
    k--;
  }
}
```




### 참고
<br/>

- 위키피디아 
  - https://ko.wikipedia.org/wiki/%ED%9E%99_%EC%A0%95%EB%A0%AC
- github 
  - https://gmlwjd9405.github.io/
  - https://github.com/gyoogle/tech-interview-for-developer
  - https://ratsgo.github.io/
- youtube
- tistory
    - https://wonjayk.tistory.com/
    - https://seanpark11.tistory.com/
