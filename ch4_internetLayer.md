1. 인터넷 계층의 역할
2. IPv4, IPv6
3. IP 어드레스의 활용
4. 라우팅
5. 라우터와 라우팅 프로토콜
6. 네트워크 오류를 통보하는 ICMP
7. 어드레스 변환
8. 도메인명
9. IP 어드레스를 자동으로 할당하는 DHCP
10. ipconfig, ping 명령
11. tracert 명령으로 통신 경로 확인하기
12. nslookup 명령으로 ip 어드레스 알아내기

### 인터넷 계층(네트워크 계층)의 역할

---

- 링크 계층과 협력해서 다른 컴퓨터에 데이터를 전달하는 역할을 한다
- IP address를 식별자 정보로 해서 데이터를 전달한다
    - 라우터를 통해 도착지를 향해 다음 경로를 연쇄적으로 찾는 라우팅 과정을 통해 목적지 경로를 찾아나간다.
- IPv4 주소 고갈을 막기 위해 private, public address를 구분하는 기법을 쓰고 Ipv6 확장주소체계를 도입하였다.
- DNS 서버를 통해 문자열 도메인명과 서비스의 IP address를 매핑해서 연결해준다.

### IPv4, IPv6

---

![1859_1.jpeg](/image/ipHeader.jpeg)

- 트랜스포트 계층에서 전달받은 세그먼트나 데이터그램에 IP헤더를 붙여 캡슐화한다.
- 네트워크 혼잡을 막기 위해 TTL(time to live) 정보를 설정해놓고, 이 기간을 초과한 패킷이 네트워크 상에서 발견되면 그 패킷을 소멸시킨다.
- 한번에 전송할 수 있는 데이터 크기를 MTU(maximum transmission unit)이라 한다. 경로상태가 좋지 않으면 이 사이즈가 줄어든다. 라우터가 데이터를 송신하기 전에 통신경로 전체의 MTU를 확인하고 이 값에 따라 패킷을 분할해서 전송한다.
- IP address 192.168.0.1 은 3개 네트워크를 표현하는 부분과 그 네트워크에 속한 1개의 호스트부 로 구성된다.
    - 라우터는 송신지 IP의 네트워크 부 정보를 보고 데이터를 보낼 목적지가 같은 네트워크인지 다른 네트워크인지 판단한다.
- IP어드레스 안에 어디까지가 네트워크부-호스트 부인지 길이를 고정해서 결정해둔 정보를 **어드레스 클래스**라고 한다.
- 어드레스 클래스는 네트워크부 길이가 미리 정해져있지만, **서브넷 마스크**를 이용하면 이 길이를 비트 단위로 유연하게 사용할 수 있다.
- **서브넷 마스크 네트워크 할당 방식**

### 라우터, 라우팅 프로토콜

---

- 라우터 역할
- 라우팅 테이블
- 라우팅 알고리즘

### 네트워크 오류 통보 프로토콜 IMCP

---

### 어드레스 변환

---

### 도메인명

---