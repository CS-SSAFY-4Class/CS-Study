# Linked List Comment

## 김한주
- 자세한 설명과 예시들로 정말 이해하기 편했습니다. 시각 자료도 많아 굉장히 편리했구요
- 리스트 탐색에 있어서 기존의 배열에 비해 장단점이 확실한 자료구조라는 생각이 드네요.
- 파이썬에서는 이 자료구조를 위한 커맨드가 따로 있을까요?(`list()`나 `tuple()`처럼요)
> 파이썬에서는 `list()`나 `tuple()`과 같이 Linked List를 위한 커맨드는 없는 거로 확인했습니다.  
> 다만 재귀나 while문으로 구현한 거를 확인했고 아래에 예시코드 적어두겠습니다.^_^  
> 
>반복문 사용  
'''python
def printNodes(node:ListNode):
    crnt_node = node
    while crnt_node is not None:
        print(crnt_node.val , end= ' ')
        crnt_node = crnt_node.next
        
printNodes(head_node)
```  

>재귀 사용  
```python
def printNodesRecur(node:ListNode):
    print(node.val, end=' ')
    if node.next is not None:
        printNodesRecur(node.next)
        
printNodesRecur(head_node)
```  

## 임준수 
- 1:1 과외를 받는것 처럼 자세하게 설명되어있어서 좋았습니다.
> 크크, 감사합니다:)

## 류정모
- node를 통해 데이터들 사이에서 연결되는 느낌과 데이터를 추가하고 제거하는 방법이 저희가 배운 Tree의 느낌을 조금 받았습니다.
- 그럼 디스크 조각 모음을 실행하는 이유가 링크 리스트의 경우 단점인 여분의 메모리를 잡아먹기 때문일까요? 아니면 Arraylist, linklist와는 다른 메로리 문제인 것일까요??
