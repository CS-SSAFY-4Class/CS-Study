# HTTP 요청 메소드(HTTP Request Methods)

## HTTP 요청 메소드란?

인터넷은 서로 다른 서버에서 호스팅되는 방대한 리소스 배열을 자랑한다. 

이러한 리소스에 액세스하려면 브라우저가 서버에 요청을 보내고 해당 리소스를 표시할 수 있어야 한다.

HTTP는 클라이언트와 서버 간의 효과적인 통신을 위해서 요청(request) 및 응답(response)을 구성하는 데 사용되는 기본 형식이고, HTTP 요청이 전송될 때 클라이언트가 사용할 수 있는 다양한 방법을 HTTP 요청 메소드라 한다.

## HTTP 요청 메소드 사용 방법

HTTP 요청은 클라이언트 또는 어플리케이션과 서버 간의 중간 전송 방법으로 작동한다.

클라이언트는 HTTP 요청을 서버에 제출하고 메시지를 내부화한 후 서버는 응답을 다시 보낸다.

응답에는 요청에 대한 상태 정보가 포함되어 있다.

## HTTP 요청 메소드들

### GET

GET은 서버의 지정된 리소스에서 데이터를 검색하고 요청하는 데 사용된다.

GET은 가장 널리 사용되는 HTTP 요청 메소드 중 하나이다.

한마디로 정리하면, 요청 URL로 식별되는 모든 정보를 검색하는 데 사용된다.

<hr>

### HEAD

서버의 각종 정보를 확인하기 위해 사용되는 메소드이다.

GET과 동일하지만, 응답(response)에 Body가 없고 response Code와 Head만 응답받는다.
<hr>

### POST

요청된 자원을 생성하기 위해 사용되는 메소드.

POST로 정보를 전송하면 URL에 파라미터가 나타나지 않으므로 각종 데이터를 안전하게 전송하기 위해 쓰인다.
<hr>

### PUT

요청된 자원을 수정하기 위해 사용되는 메소드.
<hr>

### PATCH

요청된 자원을 수정하기 위해 사용되는 메소드라는 점에서 PUT과 같지만,

해당 자원 전체를 수정하는 PUT과 달리, PATCH는 해당 자원의 일부분을 수정한다.
<hr>

### DELETE

요청된 자원을 삭제하기 위해 사용되는 메소드이다.

클라이언트에서 서버의 자원을 삭제하도록 허가하는 것은 매우 위험한 일. 

따라서 현실에서는 대부분 비활성화 시킨다.
<hr>

### TRACE

요청 리소스가 수신되는 경로를 보여준다.

자기 앞으로 요청 메시지를 반환(루프백)을 시험할 때 사용되는 메소드이다.
<hr>

### CONNECT

프락시 기능을 요청할 때 사용되는 메소드이다.
<hr>

### OPTION

웹서버에서 지원하는 메소드를 알기 위해 사용되는 메소드이다.

<hr>

## GET과 POST 의 차이점

이상 HTTP 요청 메소드의 종류에 대해 알아보았다.

하지만 현실에서는 보안 등 여러 가지의 이유로 GET과 POST 를 가장 많이 사용한다.

따라서, 두 메소드를 비교하고자 한다.

|<b>GET</b>|<b>POST</b>|
|---|---|
|<b>GET</b>|<b>POST</b>|
|<b>GET</b>|<b>POST</b>|
|<b>GET</b>|<b>POST</b>|
|<b>GET</b>|<b>POST</b>|
|<b>GET</b>|<b>POST</b>|
|<b>GET</b>|<b>POST</b>|
|<b>GET</b>|<b>POST</b>|