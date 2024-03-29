# HTTP Status Code


HTTP response status code는 특정 HTTP request이 성공적으로 완료되었는지 여부를 알려준다.
응답은 5개의 그룹으로 나뉜다:
   1. 정보를 제공하는 응답(1__),
   2. 성공적인 응답(2__),
   3. 리다이렉트(3__),
   4. 클라이언트 에러(4__),
   5. 서버 에러(5__)


## 정보 응답(1__)
`1`로 시작하는 경우 서버가 요청을 받았으며, 서버에 연결된 클라이언트는 작업을 계속 진행하라는 의미.

100 Continue  

    서버가 요청의 헤더를 받았고 클라이언트가 요청의 바디를 보내고자 할 때,
    클라이언트의 헤더 요청에 대해 서버가 지금까지의 상태가 괜찮으므로 계속해서 요청하도록 알려주는 코드.


101 Switching Protocol

    요청자가 프로토콜을 변경하도록 요청할 때 서버에서 프로토콜을 변경할 것임을 알려주는 코드.


102 Processing  

    이 코드는 서버가 요청을 수신하였으며 이를 처리하고 있지만, 아직 제대로 된 응답을 알려줄 수 없음을 알려준다.


## 성공 응답(2__)


200 OK  

    요청이 성공되었다. request method에 따라 성공의 내용이 달라진다. 가장 많이 보는 응답.  
    
  - Get: 리소스를 불러와서 메시지 바디에 전송되었습니다.  
    (The resource has been fetched and transmitted in the message body.)
  - HEAD: 
    (The representation headers are included in the response without any message body.)
  - Put or Post:
    (The resource describing the result of the action is transmitted in the message body.)
  - Trace: 
    (The message body contains the request message as received by the server.)


201 Created  

    요청이 성공적이며 그 결과 새로운 리소스가 생성되었다. 일반적으로 POST 요청 또는 일부 PUT 요청 이후에 온다.


202 Accepted 

    요청을 수신하였지만 그에 응하여 행동할 수 없다는 의미.
    이 응답은 요청 처리에 대한 결과를 이후에 HTTP로 비동기 응답을 보내는 것에 대해 명확하게 명시하지 않는다.  


204 No Content 

    요청에 대해 보내줄 수 있는 콘텐츠가 없지만, 헤더는 의미있을 수 있다.


205 Reset Content 

    요청을 완수한 이후에 사용자 에이전트에게 이 요청을 보낸 문서 뷰를 리셋하라고 알려준다.


206 Partial Content  

    클라이언트에서 복수의 스트림을 분할 다운로드하고자 범위 헤더를 전송했기 때문에 사용된다.


## 리다이렉트(3__)


300 Multiple Choice  

    요청에 대해 하나의 이상의 응답이 가능하다. 사용자는 그 중 하나를 반드시 선택하여야 한다.


301 Moved Permanently 

    요청한 리소스의 URI가 변경되었음을 의미한다. 새로운 URI가 응답에서 주어질 수도 있다.


302 Found

    요청한 리소스의 URI가 일시적으로 변경되었음을 의미한다.
    새롭게 변경된 URI는 나중에 만들어질 수 있다. 그러므로 클라이언트는 향후 요청도 반드시 동일한 URI로 해야 한다.


303 See Other  

    클라이언트가 요청한 리소스를 다른 URI에서 GET 요청을 통해 얻어야 할때, 서버가 클라이언트로 직접 보내는 응답.


304 Not Modified  
  
    이것은 캐시를 목적으로 사용된다.
    클라이언트에게 응답이 수정되지 않았음을 알려주며 클라이언트는 계속해서 응답의 캐시된 버전을 사용할 수 있다.


## 클라이언트 에러(4__)


400 Bad Request  

    잘못된 문법으로 인해 서버가 요청을 이해할 수 없음을 의미한다.


401 Unauthorized  

    비인증(unauthenticated)을 의미한다. 클라이언트는 요청한 응답을 받기 위해서 스스로를 인증해야 한다.


403 Forbidden  

    클라이언트는 콘텐츠에 접근할 권리를 가지고 있지 않다. 승인되지 않은 클라이언트의 요청에 대해 서버는 거절할 수 있다.
    401 Unauthorized 와 다른 점은 서버가 클라이언트가 누구인지 알고 있다.


404 Not Found  

    서버는 요청받은 리소스를 찾을 수 없다. 브라우저에서는 알려지지 않은 URL을 의미한다.
    이는 API에서 종점은 적절하지만 리소스 자체는 존재하지 않음을 의미할 수 있다.


405 Method Not Allowed  

    요청한 메소드는 서버가 알고 있지만, 타겟 리소스에 대해선 지원되지 않는 메소드임을 알려준다.
    예를 들어 API는 리소스를 remove하려는 DELETE 메소드를 허용하지 않는다.


406 Not acceptable  

    웹 서버가 서버 주도 콘텐츠 협상을 수행한 후 사용자 에이전트가 지정한 기준에 맞는 내용을 찾지 못할 때 전송된다.


408 Request Timeout

    이 응답은 요청한 지 시간이 오래된 연결에 일부 서버가 전송하며, 서버가 사용되지 않은 연결을 끊고 싶어하는 것을 의미한다.
    이 응답은 Chrome Firefox27+ 등 웹서핑 속도를 올리기 위해 몇몇 브라우저가 자주 사용한다.


## 서버 에러(5__)


500 Internal Server Error  

    서버가 처리 방법을 모르는 상황이 발생했다.


501 Not Implemented

    서버가 요청을 이행하는 데 필요한 기능을 지원하지 않음을 의미한다.


502 Bad Gateway

    서버가 요청을 처리하는 데 필요한 응답을 얻기 위해 게이트웨이로 작업하는 동안 잘못된 응답을 수신했음을 의미한다.


503 Service Unavailable

    서버가 요청을 처리할 준비가 되지 않았다. 일반적으로 해당 오류의 원인은 유지보수를 위해 작동이 중단되거나 과부하가 걸린 서버이다.


504 Gateway Timeout

    웹페이지를 로드하거나 브라우저에서 다른 요청을 채우려는 동안 한 서버가 액세스하고 있는 다른 서버에서 적시에 응답받지 못했음을 의미한다.


## Reference

- https://developer.mozilla.org/ko/docs/Web/HTTP/Status