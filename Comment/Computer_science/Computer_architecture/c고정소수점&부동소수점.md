# 고정소수점 & 부동소수점 Comment

## 김한주

IEEE란 말이 부동소수점에서 자주 나오던데 이 용어가 무엇을 뜯하는 말인가요?  
    - IEEE는 Institute of Electrical and Electronics Engineers라고 하는 전기전자공학 전문가들의 국제조직을 말하고 있습니다. I triple E라고 불리고 있죠. 이 국제조직에서 주요 표준 및 연구 정책을 발전하고 있는다. 산업 표준 회의를 통해서 표준을 정하고 공표하여 전반적인 산업에서의 표준화를 말합니다. 고정소수점, 부동소수점에서의 754 역시 기준을 저 회의에서 표준화를 시켰다라고 공표했다라고 생각해주시면 될 것 같습니다.  
      
지수가 부동소수점에서의 크기를 뜻한다고 되어있는데 이 크기가 '0.0001일 경우 지수는 4이다'로 받아들이면 될까요?
    - 0.0001은 부동 소수점으로 표현된 것이 아니라  지수부분을 바로 해석하시는 건 아닙니다. 먼저 전체의 숫자를 2진수로 바꾸고 그 이후에 부동소수점으로 변환시킬 수 있게 됩니다.
    0.0001
    0 01110010 00000001000111101011100
    0.00111001000000001000111101011100
    (숫자가 너무 커서... 인터넷의 도움을 받았습니다.) 
    
    표현하는 방식은 본문 글에다가 추가로 더해주겠습니다.

## 박원서

부동 소수점 부분의 지수가 실제 실수부를 나타낸다면 11bit는 오히려 고정소수점 보다 작은 것 아닌가요..? 가수부로 실수 크기를 나타낸다 하였는데 어떻게 나타내는 것 인지, 어떤 수를 예시로 드셔서 부동 소수점을 만드신 건지, 왜 갑자기 `0.0~` 이 나오는지 잘 모르겠습니다..ㅠㅠ 수학 어렵네요..

