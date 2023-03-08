# Bubble Sort(버블 정렬)
<br>

- 정의 : 원소가 거품처럼 올라오는 듯하여 버블 정렬이라고 불리게 되었다.<br/>
- 정렬 방식 : 인접한 두 개의 원소를 비교하며 자리를 계속 교환하는 방식<br/>
- 정렬 과정(ex)
    - 첫 번째 원소부터 인접한 원소끼리 계속 자리를 교환하면서 맨 마지막 자리까지 이동한다.
    - 한 단계가 끝나면 가장 큰 원소가 마지막 자리로 정렬된다.
- 시간복잡도 :  O(n**2)<br/>
<br/>

## 장단점
- 장점 : 구현이 간단하다.
- 단점 : 배열이 길어질수록 효율이 떨어진다.
<br/>
<br/>

- 이동 방법

```
[4, 5, 3, 2, 1]         5부터 이동 시작 

[4, 3, 5, 2, 1]

[4, 3, 2, 5, 1]

[4, 3, 2, 1, 5]         이동된 숫자 5

[3, 4, 2, 1, 5]         4 이동 시작 

[3, 2, 4, 1, 5]

[3, 2, 1, 4, 5]         이동된 숫자 4, 5

[2, 3, 1, 4, 5]         3 이동 시작 

[2, 1, 3, 4, 5]         이동된 숫자 3, 4, 5

[1, 2, 3, 4, 5]         2 이동 시작 

[1, 2, 3, 4, 5]         이동된 숫자 1, 2, 3, 4, 5

```
![image](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7044f3d1-012a-44ab-9113-5ebdf81ca1d6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230307T133607Z&X-Amz-Expires=86400&X-Amz-Signature=129b9be8433b7d342dfad11d391bfa92eac90584730f823f6917027a109425f5&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
- thanks to NAVER DICTIONARY 
<br/>  
<br/> 

## 구현해보기  
  
  
- python

```python
def bubble_sort(numbers):
    count = len(numbers)

    for i in range(count - 1):

        for j in range(count - i - 1):
            if numbers[j] > numbers[j + 1]:
                numbers[j], numbers[j + 1] = numbers[j + 1], numbers[j]
                
    return numbers

```  
<br/>  
<br/>  

- java  

```java
void bubbleSort(int[] arr) {
    int temp = 0;
	for(int i = 0; i < arr.length; i++) {
		for(int j= 1 ; j < arr.length-i; j++) {
			if(arr[j-1] > arr[j]) {
				temp = arr[j-1];
				arr[j-1] = arr[j];
				arr[j] = temp;
			}
		}
	}
	System.out.println(Arrays.toString(arr));
}
```  
<br/>    
<br/> 
  
## bubble_sort video
- visualiztion
    - https://www.youtube.com/watch?v=Cq7SMsQBEUw
- bubble_sort dance
    - https://www.youtube.com/watch?v=Iv3vgjM8Pv4


### Thanks to
- gyoogle github
- wikipedia
- NAVER Dictionary
- Youtube
