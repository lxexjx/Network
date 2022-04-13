
# Network

모든 html,이미지+ 앱과 서버가 통신할 때 + 서버와 서버가 통신할 때도 http프로토콜 위에서 주고 받음.

***
### 1. 인터넷 네트워크 
***

### [IP]
IP (인터넷 프로토콜): 지정한 IP주소로 메세지를 전달 할 수 있도록 정해놓은 최소한의 규칙, 패킷이라는 단위로 전달.
*IP패킷 규칙이란? 나의 IP와 목적지 IP를 적어서 IP 패킷을 만들어서 넣고 메세지를 넣고 인터넷 망에 던지다보면 노드를 통해 목적지 IP 주소까지 도착.

IP프로토콜의 한계
1. 비연결성 : 패킷받을 대상이 없거나 서비스 불능 상태여도 전송
2. 비신뢰성 : 패킷이 사라지거나 여러개 보낼 때 순서대로 안올수도 있음.
3. 프로그램 구분 : 같은 IP에서 여러 애플리케이션이 사용한다면 어떻게 구분할 것인지(ex. 끊어서 보낼 시에 중간에 다른 노드를 탈 수 있음)

socket라이브러리를 통해서 os계층에 메세지를 넘겨, 그러면 os계층에서 메세지에다가 TCP정보를 한번 씌우고 또 한칸 내려서 IP와 관련된 데이터들을 씌워(IP패킷 생성). 그후에 네트워크 인터페이스를 통해서 랜카드를 통해서 나가.

*이더넷프레임 :  물리적인 정보 포함. 

 

1.IP패킷 정보: 출발지와 목적지 IP를 넘겨.
2.TCP/IP패킷 정보 : TCP 와 관련된 정보가 들어감. 출발지, 목적지 port와 순서,검증.. 과 관련된 정보가 들어감(IP만으로 해결이 안됐던 )


### [TCP] 전송제어 프로토콜

1. 연결지향적 : 일단 연결을 하고 메세지를 보내
2. 데이터 전달 보증 : 메세지 패킷이 중간에 누락되면 내가 알 수 있음. 
3. 순서 보장 

그래서 TCP는 신뢰할수 있는 프로토콜이며 현재 대부분 사용함.


1.연결지향적 :TCP/IP프로토콜로 연결하면 
  1)클라이언트에서 서버로 syn이라는 메세지를 보내
  2) 서버에서 ack(알았다)라는 메세지를 보내면서 나도 연결해줘(syn)라는 메세지 보내
  3) 클라이언트가 알았다고 ack보내, 서로syn을 보낸거지.양쪽다 ack한거고 
  이렇게 3-hand shake하면 서로 믿을수 있고 연결됐다고 인식함. 그 다음에 데이터를 주고 받아 

2. 데이터 전달 보증
 TCP가 붙게 되면 데이터를 전송하면 서버에서 잘 받았다고 보내줘, 그래서 클라이언트가 메세지가 잘 전달됐는지 확인가능

3. 순서 보장 
 패킷1,2,3 순으로 보내냈는데 1,3,2순으로 도착하면 다 버리고 2번부터 다시 보내.(왜냐면 TCP/IP정보에 전송, 제어, 검증 정보가 다 있기 때문에)
 
 
 ### [UDP]

연결지향적이지도 데이터 전달 보증하지도 순서 보장하지도 않음.  IP와 거의 비슷하지만 port가 추가됨
port란? 내 ip로 여러 패킷이 오면 구분할 때 사용. 
데이터 양도 적고 속도도 빨라서 원하는 애플리케이션 레벨에서 최적화 가능.


### [port]
클라이언트 pc가 한번에 여러 개의 서버와 통신하면 각각 패킷들이 클라이언트에 오는데 게임에서 필요한 패킷인지, 화상통화에서 필요한 패킷인지 알수 없어. 어떻게 구분할 것인가
IP에 PORT라는 개념을 더해

IP는 목적지의 서버를 찾는것, PORT는 서버안에서 돌아가는 애플리케이션들을 구분하는 것

### [DNS]
IP는 기억하기 어렵거나 변경되면 접근불가~  중간에 

### 정리

IP : 메세지를 보내기 위해 필요.
TCP : IP로는 메세지 잘 도착 신뢰 어려워서 TCP가 해결.
UDP : IP +PORT
PORT : 같은 IP안에서 통신할 애플리케이션 구분.
DNS : 어려운 IP대신 도메인 명을 등록해서 사용하도록.



***
### 2. URI와 웹 브라우저 요청 흐름
***
URI (리소스를 식별하는 통합된 방법)
URL(리소스의 위치)
URN(리소스의 이름)
 
### [URI]

U 리소스를 식별하는 통일된 방식
R URI 로 식별할 수 있는 모든~ 것
I 식별하는데 필요한 정보

### [URL]
리소스가 있는 위치를 지정

### [URN]
리소스의 이름을 부여 but거의 사용x
-->URI==URL

### [URL문법]
*scheme://[userinfo@]host[:port][/path][?query][#fragment]*
1. scheme : 주로 프로토콜 사용 ex)http, https, ftp 등
2. userinfo : URL에 사용자 정보를 인증시에 사용하는데 거의 안씀.
3. host : 호스트명으로 도메인 명이나 ip주소를 직접 사용
4. port : 생략가능. 
5. path : 리소스가 있는 계층적 구조의 경로. ex) /members/100
6. query : key=value 형태. ?로 시작, &로 추가 가능
7. fragment : html 내부 북마크 등에 사용

### [HTTP메세지 전송]

1. 애플리케이션에서 웹브라우저가 HTTP메세지 생성
2. 소켓 라이브러리를 통해서 OS에 (TCP/IP계층)전달. 찾은 ip,port로 syn/ack해서 서버와 연결하고 데이터 전달
3.TCP/IP에서 팩해서 한번 씌우고 (IP,PORT정보 들어있음) 인터넷에 들어가->인터넷 노드를 통해 전달

구글 서버는 요청 패킷이 도착하면 TCP/IP까서 버리고 HTTP메세지를 꺼내서 해석하고-> HTTP응답 메세지를 만들어서 보내


***
### 3. HTTP 기본
***
### [HTTP]
HyperText Transfer Protocol : 문서간의 링크를 통해서 연결하는 html을 전송하는 프로토콜
거의 모든 형태의 데이터 전송 가능

 
### [Stateful, Stateless]

 1. 클라이언트와 서버 구조
  http는 클라이언트가 http메세지를 통해서 보내고 서버에서 응답이 올때 까지 기다려. 서버가 요청에 대한 결과를 만들어서 응답해
  *클라이언트와 서버를 분리하는게 중요*
  비지니스 로직이랑 데이터는 서버에 넣고 클라이언트는 UI와 사용성에 집중-> 클라이언트와 서버가 독립적으로 진화


2. 무상태 프로토콜
  서버가 클라이언트 상태를 보존하지 않는다.
    *Stateful : 상태를 유지한다. (로그인). 최소한으로만 사용
      서버가 클라이언트 이전 상태를 보존한다. -> 중간에 상태가 변경되면 장애가 발생
      중간에 다른 점원으로 바뀔 때 상태 정보를 다른 점원에게 미리 알려줘야됨.
      애초에 처음부터 정보를 다 담아서 보내고 그냥 2번에 보내면 됨.
  *Stateless : 상태를 유지하지 않는다. (단순 화면)
    서버가 클라이언트의 상태를 보존하지 않는다. -> 고객이 필요한 정보를 그때 그때 다 넘겨줘서 중간에 바뀌어도 문제없
    갑자기 고객이 증가해도 점원을 대거 투입 가능하고 갑자기 클라이언트 요청이 증가해도 서버를 대거 투입 가능.
    응답 서버를 쉽게 바꿀 수 있음-> 무한한 서버 증설 가능


### [비연결성]

1,2,번이 요청을하고 응답을 받고 3도 요청을 하고 응답을 받는동안 1,2번은 연결이 유지
다시 1번이 새로운 요청을 하면 서버가 응답
 단점: 2,3 클라이언트가 놀고 있어도 계속 연결을 유지해야됨. 
TCP/IP연결을해서 요청을 하고 응답을 받아
응답 다 받았으면 연결 끊어버려
자원 요청을 주고 받을 때만 연결하고 끊어버려서 서버를 유지하는 자원을 최소한으로 줄여

=> http는 기본적으로 연결을 유지하지 않는 모델로 빠른속도로 응답. 서버 자원을 효율적 사용 가능
     but, 중간에 다른거 하면 TCP/IP를 새로 연결 해야돼 -> 3 way handshake 시간 추가
요청하고 응답하고... 연결을 유지해


### [HTTP메세지]

1. 시작 라인
  * 요청 메세지(request-line) - HTTP method(GET: 조회), request-target(path), HTTP-version 
                       HTTP method - GET:서버에게 리소스를 달라고 해/POST: 요청한것들 처리해줘...
                       path 절대경로+ 쿼리

  *응답 메세지(status-line) - HTTP-version, status-cod, reason-phrase CRLF

2. 헤더 라인 : HTTP 전송에 필요한 모든 부가정보 들어있음.
    메세지 바디를 제외하고 필요한 메타정보 다 들어있음.
3. 메세지 바디 라인 : 실제 전송할 데이터


***
### 4. HTTP 메서드
***
### [HTTP API]

리소스란? 회원이라는 개념 그 자체
리소스 식별 중요!! 등록,수정, 삭제는 배제.  => 회원 리소스를 URI에 매핑

*요구사항- 회원 정보 관리 API  URI 설계* 
    회원 목록 조회 /read-member-list -> 회원 목록 조회 /members
    회원 조회 /read-member-by-id ->     회원 조회 /members/{id}
    회원 등록 /create-member ->          회원 등록 /members/{id}
    회원 수정 /update-member ->         회원 수정 /members/{id}
    회원 삭제 /delete-member ->          회원 삭제 /members/{id}



URI는 리소스만 식별!
리소스와 해당 리소스를 대상으로 하는 행위을 분리(회원과 행위를 분리)
->행위(메서드)는 어떻게 구분하는가? HTTP메서드가 해줘 따라서 리소스만 식별하면 됨

 

### [HTTP 메서드] 클라이언트가 서버에 요청할때 기대하는 행동

1. GET: 리소스 조회
 필요한 파라미터를 쿼리를 통해서 전달
 클라이언트가 /100달라고 요청하면 서버에 get메서드가 도착해서 내부에 db조회해서 json형식으로 data 만들어서 응답메세지를 만들어서 보내
 
2. POST: 요청 데이터 처리, 주로 등록에 사용
  클라이언트에서 서버에 메세지 바디를 통해 요청보낼 때 요청 정보를 처리해줘~  주로 신규 리소스 등록, 프로세스 처리에 사용

  /members라는곳에 리소스를 전달해. /members가 오면 서버는 그 data를 저장하는데
  서버에서 이 data를 받아서 db에 등록하고 신규 리소스 식별자 생성됨
  그래서 서버는 클라이언트에 응답 데이터를 보내


  1) 새 리소스를 생성,등록
  2) 요청 데이터 처리
           * POST의 요청 데이터 처리?
             리소스 URI에(ex. /members에) POST요청이 오면 요청을 어떻게 처리할 지 리소스마다 스스로 정리함.
  3) 다른 메서드로 처리하기 어려운 경우
3. PUT: 리소스를 '완전히'대체, 해당 리소스가 없으면 생성

클라이언트가 리소스를 식별!!(/members/100이라는 구체적인 리소스를 알고 있고 URI를 지정)<->POST와의 차이점

클라이언트 : /members/100에 리소스를 넣을거야 지정하고 data보내는데 이미 /100에 있으면 리소스 대체

신규 리소스 생성

기존 리소스를 삭제하고 완전히 덮어버림. username필드 삭제됨
4. PATCH: 리소스 부분 변경

age 부분만 변경
5. DELETE: 리소스 삭제


### [HTTP메서드의 속성]

1. 안전 : 호출해도 리소스를 변경하지 않는다.(여러번 호출했을때 변경이 일어나는 것은 안전하지 않음)

2. 멱등 : 한번 호출하던 백번 호출하던 결과는 모두 똑같.

   똑같은 요청을 2번해도 괜찮아서 자동 복구 메커니즘을 사용 가능. 외부 요인으로 중간에 리소스가 변경된는건 고려x.

          POST: 멱등이 아니다! 두 번 호출하면


### [데이터 전달 방식]

1.쿼리 파리미터를 통해
   GET

2.메세지 바디를 통해
  POST, PUT, PATCH

 

### [클라이언트에서 서버로 데이터 전송]


1.정적 데이터 조회 - 이미지나 정적텍스트 문서, GET사용, 쿼리 파라미터 없이 리소스 경로로 단순 조회 가능
경로가 /star.jsp면 서버에서 그 이미지를 클라이언트에 내려줘. 추가적인 데이터를 내려주는게 없어.단순히 URI 경로만 넣으면 받아서 이미지 리소스를 클라이언트에 내려줘. 

 
2.동적 데이터 조회 - 주로 검색,게시판 목록, 데이터 조회시 GET이나 
HTTP메세지가가 만들어져서 (GET /search?q=hello&hl=ko HTTP/1.1 Host: www.google.com) 전달하면 서버에서 받아서 쿼리 파리미터를 가지고 key&value를 꺼내서 결과를 응답해줘.
 
3.HTML Form데이터 전송
웹브라우저가 폼의 데이터를 읽어서 HTTP메세지를 생성해줘
Content-Type: application/x-www-form-urlencoded 이 값이디폴트 값. form의 메세지를 메세지 바디에 ket&value형식으로 (쿼리마라이터 처럼)보내줌. 전송 데이터를 url emcoding처리함. 
키&밸류스타일로 데이터를 만들고 http바디에 넣고 쿼리파라미터와 동일한 방식으로 서버에 전송

get으로 바꿔서 보내면 (get은 메세지 바디를 안쓰겠지!) 쿼리 파라미터에 넣어서 서버에 전달

get은 리소스 변경하면 안돼!~
파일같은거 전송할 때 웹브라우저가 경계를 잘라서
 

4. HTTP API 전송
클라이언트에서 서버로 데이터 바로 전송
서버 to 서버,앱 클라이언트,웹 클라이언트(html에서 form대신 자바스크립트로 통신:AJAX)


### [HTTP API]

<회원 관리 시스템>
API 설계 - POST 기반 등록
• 회원 목록 /members -> GET
• 회원 등록 /members -> POST
• 회원 조회 /members/{id} -> GET
• 회원 수정 /members/{id} -> PATCH, PUT, POST
• 회원 삭제 /members/{id} -> DELETE
POST-신규자원등록

1) 클라이언트는 등록될 리소스의 URI를몰라
  회원데이터로 서버에 던지면 '서버'가 알아서 회원 저장하고 식별할 수 있는 URI만들어줘.

2) 서버가 새로 등록된 리소스 URI를 생성

3) 컬렉션이란?
서버가 관리하는 리소스 디렉토리로 서버가 리소스의 URI를 생성하고 관리함.여기서 컬렉션은 /members


<파일 관리 시스템>
API 설계 - PUT 기반 등록
• 파일 목록 /files -> GET
• 파일 조회 /files/{filename} -> GET
• 파일 등록 /files/{filename} -> PUT
• 파일 삭제 /files/{filename} -> DELETE
• 파일 대량 등록 /files -> POST
   PUT-신규자원등록

1) 클라이언트가 리소스 URI를 알고 있어야 한다.
  파일 등록 시 /files/{파일이름}을 넣어준다? : 이 uri를 클라이언트가 알고있다!-> PUT
  PUT /files/star.jpg 

2) 클라이언트가 직접 리소스의 URI를 지정한다.
cf.post는 /members에 데이터 보내면 서버가 알아서 회원 id만들고 uri경로도 알아서 만들어서 내려줬음.(클라가 서버에 요청하는 것!)
put은 uri를 다 알고 등록해. 클라이언트가 직접 관리

3) 스토어(Store)란?
  클라이언트가 관리하는 리소스 저장소
  클라이언트가 리소스의 URI를 알고 관리. 스토어는 /files



<HTML FORM 사용>
회원 목록 /members -> GET
회원 등록 폼 /members/new -> GET
회원 등록 /members/new, /members -> POST
회원 조회 /members/{id} -> GET
회원 수정 폼 /members/{id}/edit -> GET
회원 수정 /members/{id}/edit, /members/{id} -> POST
회원 삭제 /members/{id}/delete -> POST
get,post만 사용

BUT 컨트롤 URI란?제약이 있어 POST의 /new, /edit, /delete가 컨트롤 URI이렇게 사용


### [정리]

• HTTP API - 컬렉션 : POST 기반 등록 , 서버가 리소스 URI 결정 많이 써~
• HTTP API - 스토어 : PUT 기반 등록 ,클라이언트가 리소스 URI 결정
• HTML FORM 사용 : 순수 HTML + HTML form 사용 , GET, POST만 지원

***
### 6.HTTP 상태코드
***

### [상태코드]

클라이언트가 서버에 요청을 보내면 그 요청이 잘 처리가 됐는지 http response가 올 때 알려주는 기능

• 1xx (Informational): 요청이 수신되어 처리중

• 2xx (Successful): 요청 정상 처리 200,201,

• 3xx (Redirection): 요청을 완료하려면 추가 행동이 필요 클라이언트가 서버에 요청하면 추가적인 조치가 필요해 클라에 다시 돌려보내

• 4xx (Client Error): 클라이언트 오류, 잘못된 문법등으로 서버가 요청을 수행할 수 없음

• 5xx (Server Error): 서버 오류, 서버가 정상 요청을 처리하지 못함
 

### [2xx] - 성공

201 - 클라이언트가 요청한것을 서버쪽에서 리소스 생성. post로 등록했을 때 
202 - 요청이 접수는 됐다
204 - 성공은 했고 돌려보낼 뭐가 없음



### [3xx] - 리다이렉션
cf.리다이렉션이란?  웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동

더이상 안쓰는 /event로 들어오면 바뀐 /new-event로 서버로 다시 요청해
1. 영구 리다이렉션 - 특정 리소스의 URI가 영구적으로 이동 ex) /members -> /users ex) /event -> /new-event 

  원래 url을 더이상 사용하면 안됨. 서버기 url 경로를 바꿔서 응답보내

  301 - ex)post요청했는데 get으로 변경될 수 있음
  308 - ex) 301과 동일하나 리다이렉트 요청 시 똑같이 post로 보내고 http바디 유지

301로 응답 코드를 보내서 클라이언트에서 url의 경로를 /new-evenet로 바꿔서 GEt!!으로 변경해
등록하려고 post로 보냈지만 get으로 /new-event로 날아가고  메세지 바디 부분이 다 사라져서 새로운 이벤트 페이지 처음 부터 입력하게됨.
->308로 해결 하게됨 

다시 클라이언트에서 서버로 보낼 때는 POST로 보내서 메세지 본문 유지시켜줘
 

2. 일시 리다이렉션 - 일시적인 변경, 주문 완료 후 주문 내역 화면으로 이동, PRG: Post/Redirect/Get
  주문 완료하고 주문 내역 하면으로 이동 
   302 - 리다이렉트시 요청 메서드가 get으로 변하고 본문이 제거 가능성 있음(거의 301)
   307 - 리다이렉트시 요청 메서드와 본문 절대 유지
   303 - 302와 비슷 하지만 리다이렉트시 요청 메서드가 get으로 변경

* PRG(Post/Redirect/get) 

post로 주문후에 웹브라우저 새로 고침하면 post의 데이터가 한번 더 서버에 중복주문 들어갈 수 있음. 마지막 요청은 post
1)/order에 주문을 하면 
2)주문 db에 마우스 하나저장 3)ok보내고
4)마지막 요청은 post인데 실수로 새로고침하면 
5)post요청을 또 다시 보내 6) 그러면 주문 데이터 한 건이 더 들어와 7)주문 완료 응답이 옴



해결책
=>POST로 주문후에 새로 고침으로 인한 중복 주문 방지, POST로 주문후에 주문 결과 화면을 GET 메서드로 리다이렉트 , 새로고침해도 결과 화면을 GET으로 조회 , 중복 주문 대신에 결과 화면만 GET으로 다시 요청
 

1)/order에 주문을 하면
2)주문 db에 마우스 하나저장 3)200이 아닌 302 found 보내고
4) get으로 바꿔 5)주문을 db를 쌓는게 아닌 19번을 조회해서 html 화면 만들어서 7)ok

 
정리
  302 Found -> GET으로 변할 수 있음  (이거 주로 써)
  307 Temporary Redirect -> 메서드가 변하면 안됨
  303 See Other -> 메서드가 GET으로 변경
 

3. 특수 리다이렉션 - 클라이언트에서 캐시가 만료돼서 클라이언트가 서버에 캐시 관련 정보를 넘겨줘. 결과 대신 캐시를 사용


### [4xx] - 원인은 클라이언트 오류. 클라이언트가 이미 잘못된 요청, 데이터를 보내고 있기 때문에, 똑같은 재시도가 실 패

  401 - 클라이언트가 해당 리소스에 대한 인증이 필요
  403 - 서버가 요청을 이해했지만 승인을 거부, 인증 자격 증명은 있지만, 접근 권한이 불충분한 경우
  404 - 요청 리소스가 서버에 없음

 

### [5xx] -  원인은 서버 오류. 진짜 심각한 오류가 있는게 아니고서야 정말 내면 안됨.

  503 -  서버가 일시적인 과부하 또는 예정된 작업으로 잠시 요청을 처리할 수 없음
  500 - 애매하면 그냥 이거

***
### 7.HTTP 헤더- 
***

### [HTTP 헤더]

header 필드= field-이름 ":" OWS field-value OWS
HTTP 전송에 필요한 모든 부가정보


헤더 분류(과거)
 • General 헤더: 메시지 전체에 적용되는 정보, 예) Connection: close
 • Request 헤더: 요청 정보, 예) User-Agent: Mozilla/5.0 (Macintosh; ..)
 • Response 헤더: 응답 정보, 예) Server: Apache
 • Entity 헤더: 엔티티 바디 정보, 예) Content-Type: text/html, Content-Length: 3423


      메시지 본문(message body)은 엔티티 본문(entity body)을 전달하는데 사용

      엔티티 본문은 요청이나 응답에서 전달할 실제 데이터

      엔티티 헤더는 엔티티 본문의 데이터를 해석할 수 있는 정보 제공 

      데이터 유형(html, json), 데이터 길이, 압축 정보 등등

-

### [표현] 엔티티(Entity) -> 표현(Representation), 표현 메타데이터 + 표현 데이터

• Content-Type: 표현 데이터의 형식
    회원 리소스를 html형식(표현)으로 보낼건지, json표현으로 보낼건지    컨텐트 바디에 들어가는게 뭔지
    ex) text/html; charset=utf-8, application/json, image/png

• Content-Encoding: 표현 데이터의 압축 방식
    회원 데이터의 압축 방식, 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
    ex) gzip, deflate, identity

• Content-Language: 표현 데이터의 자연 언어
    이 표현 언어가 본문에 영어인지 한국어인지

• Content-Length: 표현 데이터의 길이

 
### [협상] - 클라이언트가 원하는 표현으로 달라고 서버에 요청


클라이언트가 서버에 요청할 때 선호하는 언어는 한국어라고 보내면 서버에서는 메세지 바디에 한국어 넣어서 보내
 

Quality Values(q) 값 사용 : 0~1, 클수록 높은 우선순위, 생략하면 1, 구체적인 것이 우선


### [전송방식]

1. 단순 전송
메세지 바디에 대한 content-length를 길이를 알아 지정해, 한번에 요청하고 한번에 받아

2. 압축 전송
뭘로 압축되었는지

3. 분할 전송
용량이 커서 한번에 보내면 시간 걸리니가 조개서 보내. content-length를 넣으면 안됨(계산이 안되니까)

4. 범위 전송
중간에 끊기면 다시 받기 아까우니까 범위 지정해서 나머지 전송해달라고 해.
 

 
### [From] 유저 에이전트의 이메일 정보

### [Referer] 이전 웹 페이지 주소, 이전에 구글에서 들어온거구나~, 유입경로 분석 가능

### [User-Agent] 통계 정보

### [Server] 요청을 처리하는 오리진 서버(프록시 서버말고 응답해주는 진짜 서버)의 소프트웨어 정보

### [Date] 메세지가 발생한 날짜와 시간, 응답에서 사용

### [Host] 요청에서 사용함, 필수 헤더, 하나의 서버가 여러 도메인을 처리해야할 때 
/hello보냈을 때 서버는 어떤 애플리케이션에 보낼지 몰라(IP가 같아서), 그래서 호스트헤더를 넣어서 보내

### [Location] Location헤더가 있으면 Location위치로 자동 이동

### [Allow] 허용가능한 HTTP매서드

### [Retry-After] 다음 요청하기 까지 기다려야하는 시간, 날짜, 초단위 표기

### [Authorization] 클라이언트 인증 정보를 서버에 전달

### [WWW-Authenticate] 리소스 접근시 필요한 인증 방법 정의


### [쿠키]

2개의 헤더 사용
   • Set-Cookie: 서버에서 클라이언트로 쿠키 전달(응답)
   • Cookie: 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달


로그인한 상태에서 다시 웰컴페이지 들어오면 서버에서는 로그인한 사용자가 보낸건지 아닌지 몰라
 Stateless!!
   HTTP는 무상태(Stateless) 프로토콜
   클라이언트와 서버가 요청과 응답을 주고 받으면 연결이 끊어짐
   클라이언트가 다시 요청하면 서버는 이전 요청을 기억하지 못함 
   클라이언트와 서버는 서로 상태를 유지하지 않음
 

대안?

모든 요청에과링크에 사용자 정보를 포함해야됨.

홍길동을 쿠키에 말아서 응답하면 웹브라우저에서 내부에 쿠키저장소에user=홍길동을 저장해놔.

웹브라우저가 웰컴페이지 들어가면 자동으로 서버에 요청시마다 쿠키 값을 무조건 꺼내서 http헤더 만들어서 서버에 보내.
 
쿠키는 모든 요청에 정보 자동 포함됨

사용자 로그인 세션 관리 : 서버에서 세션키를 만들어서 db에 저장하고 세션값을 클라이언트에 반환해주면 클라이언트는 서버 요청시마다 세션 아이디를 보내.

최소한의 정보만 사용.

요청시마다 서버에 보내는게 아닌 클라이언트에 보관하고 필요시에만 사용하려면 웹스토리지


 

### [쿠키 생명주기]

1. Set-Cookie: expires=Sat : 만료일이 되면 쿠키 삭제

2. Set-Cookie: max-age=3600 (3600초) • 0이나 음수를 지정하면 쿠키 삭제

3. 세션 쿠키: 만료 날짜를 생략하면 브라우저 종료시 까지만 유지

4. 영속 쿠키: 만료 날짜를 입력하면 해당 날짜까지 유지

 

### [쿠키- 도메인 지정 가능]

1. 명시: 명시한 문서 기준 도메인 + 서브 도메인 포함

2. 생략: 현재 문서 기준 도메인만 적용
 

### [쿠키 - 경로]

이 경로를 포함한 하위 경로 페이지만 쿠키 접근, 일반적으로 path=/ 루트로 지정
 

### [쿠키 - 보안]

1. Secure
  • 쿠키는 http, https를 구분하지 않고 전송
  • Secure를 적용하면 https인 경우에만 전송 

2. HttpOnly • XSS 공격 방지
  • 자바스크립트에서 접근 불가(document.cookie)
  • HTTP 전송에만 사용 

3. SameSite
  • XSRF 공격 방지
  • 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송

***
### 8.HTTP 헤더 : 캐시와 조건부 요청
***
웹브라우저에서 요청하면 서버에서 총 1.1M네트워크 카지하면서  웹브라우저에 내려보내

웹브라우저에 이미지 표시됨

서버에서 또 똑가은 응답을 받아서 내려주는데 헤더와 바디부를 다시 만들어서 내려보내
 
• 데이터가 변경되지 않아도 계속 네트워크를 통해서 데이터를 다운로드 받아야 됨
• 인터넷 네트워크는 매우 느리고 비쌈
• 브라우저 로딩 속도가 느림



서버에서 이시간동안은 캐시가 유효하다는

웹브라우저 내부의 캐시 저장소에 응답결과를 캐시에 저장

두번째 요청시에는 캐시를 먼저 뒤져서

캐시에서 바로 가져와. 네트워크를 탈 필요가 없어
• 캐시 덕분에 캐시 가능 시간동안 네트워크를 사용하지 않아도 됨
• 비싼 네트워크 사용량을 줄일 수 있음
• 브라우저 로딩 속도가 매우 빠름
• 빠른 사용자 경험



60초가 초과되면 다시 요청해야됨. 서버에서 똑같은 메세지 내려줘

받은 캐시 데이터를 기존꺼 지우고 다시 캐시 덮어씌워. 캐시 초기화
캐시 유효 시간이 초과하면, 서버를 통해 데이터를 다시 조회하고, 캐시를 갱신. 다시 네트워크 다운로드가 발생

 

캐시 유효 시간 초과해서 서버에 다시 요청하면 

1. 서버에서 기존 데이터를 변경함 2. 서버에서 기존 데이터를 변경하지 않음->다시 받기 아까워

->

### [검증헤더와 조건부 요청]

캐시 만료후에도 서버에서 데이터를 변경하지 않으면 데이터를 전송하는 대신에 저장해 두었던 캐시를 재사용 할 수 있음. 단 클라이언트의 데이터와 서버의 데이터가 같다는 사실을 확인할 수 있는 방법 필요


이 데이터의 최종 수정일을 넣어줘서 응답을 내려주면

응답결과를 캐시에 저장

웹브라우저가 서버에 요청을 보낼 때 if-modified-since라는 http요청헤더를 붙여서 서버에 넘기면

데이터가 수정이 안됐으면

응답에 304보내서 (변경된게 없다!)수정된게 없어서 http바디가 없어 빼고 보내. 헤더만 보내
 


캐시 유효 시간이 초과해도, 서버의 데이터가 갱신되지 않으면 • 304 Not Modified + 헤더 메타 정보만 응답(바디X)

클라이언트는 서버가 보낸 응답 헤더 정보로 캐시의 메타 정보를 갱신, 캐시에 저장되어 있는 데이터 재활용

=>네트워크 다운로드가 발생하지만 용량이 적은 헤더 정보만 다운로드

 

### [검증헤더와 조건부 요청]

1. 검증 헤더
   • 캐시 데이터와 서버 데이터가 같은지 검증하는 데이터
   • Last-Modified , ETag

 

2. 조건부 요청 헤더 • 검증 헤더로 조건에 따른 분기
   • If-Modified-Since: Last-Modified 사용
   • If-None-Match: ETag 사용
   • 조건이 만족하면 200 OK
   • 조건이 만족하지 않으면 304 Not Modified

 

If-Modified-Since이후에 수정됐으면

 데이터 미변경 예시

    • 캐시: 2020년 11월 10일 vs 서버: 2020년 11월 10일 변경이 안일어났으니 304, 헤더 데이터만 전송(BODY 미포함)
      전송 용량 0.1M (헤더 0.1M, 바디 1.0M)

 데이터 변경 예시

    • 캐시: 2020년 11월 10일  vs 서버: 2020년 11월 10일 수정이 됐으니까 200 OK, 모든 데이터 전송(BODY 포함)
      전송 용량 1.1M (헤더 0.1M, 바디 1.0M)

 

1초미만단위는 캐시 조정 불가능, 날짜 기반의 로직이여서 전체 데이처를 다시 다운로드해,주석은 그냥 신경안쓰고 싶어


==>[ETag]

캐시용 데이터에 임의의 고유한 버전 이름을 달아둠 ex) ETag: "v1.0", ETag: "a2jiodwjekjl3"

데이터가 변경되면 이 이름을 바꾸어서 변경함(Hash를 다시 생성) ex) ETag: "aaaaa" -> ETag: "bbbbb" 

진짜 단순하게 ETag만 보내서 같으면 유지, 다르면 다시 받기!



ETag를 저장


단순하게 ETag만 서버에 보내서 같으면 유지, 다르면 다시 받기. 캐시 제어 로직을 서버에서 완전히 관리
 

### [캐시 제어 헤더]

1. Cache-Control: 캐시 제어
   • Cache-Control: max-age  캐시 유효 시간, 초 단위
   • Cache-Control: no-cache 데이터는 캐시해도 되지만, 항상 오리진 서버에 검증하고 사용
   • Cache-Control: no-store  데이터에 민감한 정보가 있으므로 저장하면 안됨 (메모리에서 사용하고 최대한 빨리 삭제)

2. Pragma: 캐시 제어(하위 호환)
3.Expires: 캐시 만료일을 정확히 날짜로 지정 가능 

 

### [조건부 요청 헤더]

If-Match, If-None-Match: ETag 사용

If-Modified-Since, If-Unmodified-Since: Last-Modified 사용

 

### [프록시 캐시]

웹브라우저가 직접 접근이 아니라 프록시 캐시 서버에 접근하도록
 


### [캐시 무효화]

1. Cache-Control: no-cache, no-store, must-revalidate 다 넣어줘
2. Pragma: no-cache 

노캐시로 보냈는데 원서버에 접근이 불가하면 프록시캐시가 오래된 데이터라도 보여주겠다하면 200으로 보내.
노캐시로 보냈는데 원서버에 접근이 불가하면 프록시캐시가 504를 보내. 통장잔고 같은거
 
