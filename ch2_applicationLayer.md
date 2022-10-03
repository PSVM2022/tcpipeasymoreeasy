1. 애플리케이션 계층의 역할
    - 프로토콜 종류
2. 웹 페이지를 전송하는 HTTP
    - 웹 페이지가 표시되기까지의 과정
    - HTTP 프로토콜 정의, stateless, 요청, URL, 응답, 상태코드
3. 웹 서비스와 웹 애플리케이션
    - HTTP 메세지 - GET, POST
    - AJAX
4. 세션을 유지하기 위한 쿠키
    - 쿠키, 세션 정의. 각각 하는 일
5. 이메일
    - 이메일 프로토콜
6. PC끼리 파일 공유하기
    - P2P
7. 파일 전송하는 FTP
    - FTP
8. 원격지의 컴퓨터 제어하기
    - Telnet, SSH
9. Voice over ip, 영상 스트리밍
    - VOIP
    - 동영상 스트리밍
10. 크롬 개발도구로 HTTP 메세지 살펴보기
    - HTTP 메세지
11. MIME
    - MIME 정의, 특징

### 애플리케이션 계층의 대표적 프로토콜 종류

---

- **HTTP - 웹 클라리언트, 서버 간의 프로토콜**
- **POP3, SMTP, IMAP - 메일 송수신, 보관**
- **FTP - 서버를 통한 파일 송수신**
- **Telnet, SSH - 원격 서버 제어**
- **DNS - 도메인:IP 정보를 서로 변환할 때 사용**
- DHCP - LAN 내의 컴퓨터에 IP 주소 할당할 때 사용
- **SSL/TLS - 통신 데이터 암호화해서 주요 정보를 주고받을 때 사용**
- NTP - 네트워크 연결 장비 간 시스템 시간 동기화
- LDAP - 네트워크 연결된 자원 통합 관리에 필요한 디렉터리 서비스 제공

### 브라우저에 주소를 입력했을 때 사이트 렌더링까지의 과정

---

1. 브라우저는 주소창 입력에 대한 요청을 대기열에 넣습니다.
2. 브라우저 캐시, 서버의 공유프록시 캐시에 결과값이 있는지 확인합니다.
    - 브라우저 캐시 - 쿠키, 로컬스토리지 등의 브라우저 자체의 캐시. 사용자가 HTTP를 통해 다운로드 하는 모든 문서를 캐싱합니다.
    - 공유프록시 캐시 - 요청한 서버의 프록시 서버가 캐싱을 하는 것입니다.
3. 메모리에 있는 호스트 파일 등의 캐시를 확인하고 캐시미스가 일어나면 브라우저가 IP주소를 확인하기 위해 DNS서버에 주소를 보냅니다. 
    - DNS: 도메인이름과 IP주소를 매핑해주는 서버. www.google.com에 DNS 쿼리가 오면 Root DNS → .com DNS → .naver DNS → .www DNS 과정을 거쳐 완벽한 주소를 찾아 IP주소를 매핑합니다.
4. IP 라우팅을 위해 ARP 로직을 거쳐 서버를 찾습니다. 
5. 초기연결을 위해 TCP 3-way handshake 과정을 거쳐 연결이 성립됩니다
6. 연결이 되면 서버로부터 HTML 문서를 수신합니다. 
7. 브라우저가 수신한 HTML문서를 렌더링합니다. 

### HTTP 특징

---

- stateless - 무상태 프로토콜이다 . 서버가 클라이언트 상태를 보존하지 않는다 ⇒ stateless이다.
- connectionless - HTTP 통신 시에 정보를 한번 씩 주고받고 바로 종료된다.

### HTTP 헤더 주요 항목

---

![Screen Shot 2022-05-05 at 20.03.30.png](/image/Screen%20Shot%202022-05-05%20at%2020.03.30.png)

- **HTTP 메서드** - GET, POST, PUT, PATCH, DELETE…
- **URL**
    - 웹페이지 주소를 받기 위해 HTTP 요청을 한다. URL 문자열로 요청한다
    - 프로토콜(https) - 호스트명(www.google.com) - 포트번호(443) - path(/search) - 쿼리 파라미터(q=hello&hl=ko)
- **세부 항목에 대한 자세한 학습이 필요**

### HTTP 메서드 - GET, POST, PUT, PATCH, DELETE

---

- **GET - 읽는다. 조회한다**
    - 성공시 200. 오류일 경우 404 NOT FOUND 혹은 400 BAD REQUEST를 반환한다.
    - 데이터를 수정, 삭제하는데 사용하면 안된다.
- **POST - 자원을 생성한다**
    - 보통 하위자원을 생성한다. book 테이블 안의 데이터를 생성한다. 성공적으로 생성되면 HTTP 상태 201을 반환한다.
- **PUT - 전체자원을 업데이트한다**
    - 요청을 보낼 때 전체를 보내야 한다. 응답으로 받는 메세지는 수정된 결괏값과 동일해야한다
- **PATCH - 일부 자원을 업데이트한다**
    - 요청을 보낼 때 수정하는 일부분을 보내야 한다. 응답으로 받는 메세지는 수정된 결괏값과 동일해야한다
    - Ex) {a: 1, b:2} 데이터를 업데이트 할때 PUT으로 수정하면 a, b의 value값을 다 보내야되지만, PATCH는 원하는 키 하나만 보낼 수 있다.
- **DELETE - 삭제한다**

### HTTP 메서드의 Idempotent (멱등성)

---

- 연산을 여러번 적용하더라도 결과가 달라지지 않는 성질이다.
- 동일한 요청을 여러번 보냈을 때의 결과가 한번 보낸 결과와 같을 때 해당 HTTP 메서드가 멱등성을 가진다고 한다. 여기서 결과는 서버의 상태를 의미한다(응답 상태코드가 아니다. 상태코드가 바뀌어도 서버의 상태가 항상 같은 상태라면 멱등성이 있다고 한다)
- GET, PUT, DELETE는 멱등성을 가지며, POST, PATCH는 멱등성을 가지지 않는다.
- HTTP 스펙의 규약이기 때문에 꼭 지키지 않아도 되지만, 지키지 않는다면 해당 API의 동작을 유추하기 힘들도 원치않는 동작을 일으킬 가능성이 있어서 지키는게 좋다.

### 세션, 쿠키

---

- HTTP는 stateless 프로토콜이기 때문에 한 유저의 여러 건의 요청 처리를 처리하기 위해 이를 동일한 접속 세션으로 처리할 수 있도록 쿠키를 이용합니다.
- 서버는 HTTP 응답에 쿠키값을 보내고, 브라우저는 이를 확인해서 저장 한 이후, 그 다음 요청때부터 서버에 자동으로 전송이 됩니다. 클라이언트, 서버 둘 다에서 조작이 가능합니다. 보통 서버에서 만료기간 등을 설정하고 컨트롤합니다. Set-Cookie 헤더에 설정된 데이터조각으로서 4kb까지 담을 수 있습니다.
- 만료기한을 지정했는 여부에 따라
    - 세션 쿠키 - 세션쿠키는 Expires 혹은 Max-Age 같은 속성을 지정하지 않은 쿠키입니다. 브라우저가 닫히면 제거됩니다.
    - 영구 쿠키 - Expires 나 Max-Age 속성을 지정해서 일정 기간이 지나면 제거됩니다. 단 브라우저가 닫혀도 만료되지 않습니다.
- `Set-Cookie: <cookie-name> = <cookie-value>`
`Set-Cookie: <cookie-name> = <cookie-value>; Expires=<date>`
`Set-Cookie: <cookie-name> = <cookie-value>; Max-Age=<non-zero-digit>`
`Set-Cookie: <cookie-name> = <cookie-value>; Domain=<domain-value>`
`Set-Cookie: <cookie-name> = <cookie-value>; Path=<path-value>`
- secure - https로만 가능하다. 그러나 크롬 52버전 이상, 파폭 52버전 이상을 포함한 일부 브라우저는 보안을 강화하고 안전하지 않은 httpt사이트가 Secure 지시문으로 쿠키를 사용하는 것을 금지하기 위해 이 사양을 무시한다
`Set-Cookie: <cookie-name> = <cookie-value>; Secure`
    1. HttpOnly - 공격자가 자바스크립트로 빼낼 수 없음(document.cookie로 접근 불가) 
    `Set-Cookie:<cookie-name> = <cookie-value>; HttpOnly`
    2. 요청이 동일한 도메인에서 시작된 경우에만 쿠키가 애플리케이션으로 전송되도록 허용한다
    `Set-Cookie: <cookie-name> = <cookie-value>; SameSite=Strict`
- 보동 쿠키에 세션ID를 담는데, 세션ID 기반으로 클라이언트의 인증정보를 알 수 없게 해야된다. 세션ID를 공격자가 추측하기 어렵게 길고 랜덤하게 생성하는 알고리즘을 써서 사용자 수에 대비해야한다. 충분히 큰 수로 하고, HttpOnly옵션, 세션 타임아웃을 걸어야한다.
- 쿠키의 시큐어 코딩 - 쿠키는 정보의 간접수집에 해당되며 KISA 등의 인증기준에 해당하는 지침을 준수해서 서비스를 구축해야한다.

### REST API

---

- **Uniform-Interface을 가집니다. 각각의 자원들이 각각 독립적인 인터페이스를 가져야 된다는 특성입니다.**
    1. 웹페이지를 변경했다고 웹브라우저를 업데이트하는 일은 없어야 합니다. 
    2. HTTP 명세나 HTML 명세가 변경되어도 웹페이지는 잘 작동해야합니다. 
- **REST API 아키텍쳐의 규칙 6가지(Representational state transfer API)**
    1. **Self-descriptive messages - HTTP header에 타입을 명시하고, 각 메세지는 MIME types에 맞춰서 표현해야합니다.** 
        - 메시지 스스로가 자신에 대한 설명을 할 수 있어야 한다.
        - JSON을 반환한다면 헤더에 application/json 타입이라고 명시해야한다. MIME types는 문서, 파일 등의 특성과 형식을 나타내는 표준이다. IETF의 RFC6638에 정의, 표준화 되어있다. ‘font/ttf’, ‘text/plain’, ‘text/csv’ 등이 있다.
    2. **HATEOAS 구조(Hypermedia As The Engine of Application State) -** **하이퍼링크에 따라 다른 페이지를 보여줘야 하며, 데이터마다 어떤 URL에서 요청했는지 명시해주어야 합니다.**
        - 데이터만 주는게 아니라 링크에 프로퍼티값을 줘서 어떠한 URL에서 보내주었는지 명시해야한다
        - Hypermedia(링크)를 통해서 애플리케이션의 상태 전이가 가능해야한다. 또한 hypermedia(링크)에 자기 자신에 대한 정보가 담겨야한다
            
            ```jsx
            // 하이퍼링크에 따라 다른 페이지를 보여준다. 데이터마다 어떤 URL에서 요청했는지 명시해준다.
            res.json(personObj, [
            	{rel: 'self', method: 'GET', href: 'http://127.0.0.1'},
            	{rel: 'create', method: 'POST', title: 'Create Person', href:'http://127.0.0.1/person'}
            ]);
            // 혹은 data 위에 링크를 쓴다.
            {'link': http://google.com/todos/{id}, "data": ['work', 'study']}
            ```
            
    3. Stateless - REST API를 제공해주는 서버는 세션을 해당 서버 쪽에 유지하지 않는다(HTTP를 쓰는 것만으롣로 만족됨)
    4. Cacheable
        - HTTP는 원래 캐시가 된다. 새로고침을 하면 304가 뜨면서 원래 로드해놨던 js와 css등을 불러온다. 네트워크 요청시 해당되는 자원을 복사해서 메모리에 저장해두었다가 같은 요청시에 네트워크 요청을 하지 않고 브라우저 메모리에 있던 자원을 다시 반환합니다.
        - HTTP 메서드 중 GET으로 받은 값으로만 한정됩니다.
        - 서버는 GET으로 받아오는 응답헤더에 `‘Cache-Control:max-age=100’` (100초) 만료시한을 정할 수 있습니다.
        - 캐싱된 데이터가 아직도 유효한지를 판단하기 위해 `‘Last-modified’`, `‘Etag’`를 씁니다. ‘Etag’는 전달되는 값에 태그를 붙여서 캐싱되는 자원이지를 확인해주는 것입니다.
    5. Client-Server 구조  - 클라이언트와 서버가 서로 독립적인 구조를 가져야합니다.
        - 서버는 API를 제공하고 그 API에 맞는 비즈니스 로직을 처리합니다. 클라이언트에서는 HTTP로 받는 로직을 처리합니다.
    6. Layered System - 계층구조로 아키텍쳐를 만들 수 있다는 뜻입니다.
        - URL 규칙 - 자원을 표기하는 URI에 규칙을 적용해야합니다.
            1. 동작은 HTTP 메서드로 해야됩니다. 
                - 동작은 조회GET 추가POST 수정PUT 삭제DELETE 로 표현해야합니다. `/books/delete/1` 이렇게 하면 안됩니다.
            2. 확장자는 표기하지 말아야합니다. .jpg, .html, .do 등…
            3. 동사가 아닌 명사로만 표기해야합니다. 
                - 유저가 책을 소유한다 를 표현한다면 `유저/유저아이디/inclusion/책/책아이디` 이렇게 구성해야합니다.
            4. URI는 계층적인 내용을 담아야합니다. 
                - `/집/아파트/전세` 이런식으로
            5. 소문자로 표현하며 너무 길 경우에는 - 하이픈을 씁니다. 
            6. HTTP 응답 상태코드를 활용합니다.