# OSI 7 계층
- OSI 7 계층이 필요한 이유
  - 서로 다른 컴퓨터 간의 통신을 위해

 | 계층  |  이름 |
|:---:|:------:|
|  7  |  응용 |
|  6  |  표현 |
|  5  |  세션 |
|  4  |  전송 |
|  3  |  네트워크 |
|  2  |  데이터링크 |
|  1  |  물리 |

### 물리 계층 (1계층)
  - 데이터와 전기적인 신호를 상황에 맞게 변환함
  - 물리적 매체를 통해서 다른시스템에 전기 신호를 전송함.
  - 데이터 접속장치: 리피터, 허브
### 데이터 링크 계층 (2계층)
- 두 노드 사이의 전송을 담당
- 데이터 단위 : `프레임`
  - 네트워크 계층의 데이터에 `이더넷 헤더`와 `트레일러`를 붙인 데이터
      - 네트워크 접속 장치 간에 신호를 주고받는 규칙을 정하는 계층 = 주로 `이더넷`을 사용함
      - 이더넷 헤더의 구조(14Byte) : `수신지 MAC 주소(6Byte)` + `송신지 MAC 주소(6Byte)` + `유형(2Byte)`
- 전송할 데이터 앞에는 헤더, 뒤에는 트레일러를 (추가/제거) 하여 (물리계층/네트워크 계층으로 전송)으로 전송한다.
- 순서제어: 프레임에 순서를 부여하여 올바른 순서로 데이터가 전송될 수 있게 함
- 흐름제어: 한번에 전송할 수 있는 데이터양을 조절
- 오류 검출 및 정정
- 데이터 접속 장치 : 스위치(플러딩(flooding), MAC 주소 필터링)
### 네트워크 계층 (3계층)
데이터 링크 계층은 인접한 두 노드 사이의 전송을 담당한다. 이때 전송하는 데이터인 `프레임`은 현재 노드와 다음 노드의 물리적인 주소를 담으며 계속 변한다. 
하지만, 네트워크 계층에서는 송신지와 최종수신지의 논리주소인 IP를 패킷에 담아서 데이터를 최종 수신지까지 전달한다.
- 논리 주소 지정: 송신지와 수신지 주소를 헤더에 포함함
- 데이터 단위 : `패킷`(`헤더(송신지IP, 수신지IP, 데이터)` + `세그먼트`)
- 주소지정, 단편화, 라우팅
- 프로토콜: IP
- 네트워크 접속장비 : 라우터, 스위치
#### IPv4
32비트를 사용하여 ip를 표현하는 방식  ex) 255.255.255.255  
<클래스 타입 / 네트워크 ID / 호스트 ID > 의 형태로 네트워크 주소를 표현한다.
- 클래스 타입
  - A 클래스 IP주소의 맨 앞이 `0`, 네트워크ID를 위해서 8비트, 호스트ID를 위해서 24비트를 사용함
  - B 클래스 IP주소의 맨 앞이 `10`, 네트워크ID를 위해서 16비트, 호스트ID를 위해서 16비트를 사용함
  - C 클래스 IP주소의 맨 앞이 `110`, 네트워크ID를 위해서 24비트, 호스트ID를 위해서 8비트를 사용함.
- 참고
  - 네트워크 주소: 호스트ID가 10진수 0인 경우
  - 브로드캐스팅 주소: 호스트ID가 10진수 10인 경우 -> 네트워크 전체에 데이터를 전송할때 사용하는 주소.
#### IPv6
128비트를 사용하여 ip를 표현하는 방식, IPv4보다 많은 주소를 표현할 수 있다. ex) FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF  
< 네트워크 주소(64비트) / 인터페이스 주소(64비트) >
- 장점
  - ipv4에비해 많은 주소를 표현할 수 있다.
  - 단순해진 헤더의 포맷: IPv4에서 불필요했던 헤더를 제거하여 보다빠른 처리가 가능함.
  - 간편해진 주소 설정 기능
  - 강화된 보안기능
  - 개선된 모바일 ip


### 전송 계층 (4계층)
송신하려는 데이터를 패킷으로 분할, 수신한 패킷을 재조립한다.
데이터 단위: 세그먼트
- 연결제어: 패킷을 하나의 경로로 보낼것인지 결정
- 수신지로 데이터 전송: 수신지에서 데이터의 모든 패킷 전송과 도착을 검사한다.
- 단편화 : 데이터를 전송가능한 단편(세그먼트)로 나누고 순서 번호를 기록한다.
- 재조립 : 수신지의 전송계층에서 순서번호에 따라 데이터를 올바르게 조립한다.

### TCP(연결형)
- 연결형
- 전이중통신방식
- 송신측과 수신측의 연결을 확립을 한 뒤 통신을 한다
- 신뢰성있는 바이트 스트림 서비스를 제공한다.
  - TCP프로토콜은 전송을 위해 바이트 스트림을 세그먼트 단위로 나눈다.
  - *세그먼트: TCP를 이용하여 두 장치간에 전달하는 데이터의 단위
  - *TCP로 전송할때 추가하는 헤더를 `TCP헤더`라고 함. TCP헤더가 붙은 데이터를 `TCP세그먼트`라고함
- 3 way handshaking
  - 신뢰할 수 있는 연결을 위해서 패킷요청을 3번 교환하는 것으로, 데이터를 전송하기 전에 일어난다.
  1) 송신측 컴퓨터에서 수신측 컴퓨터에 연결허가를 받기 위해 `SYN요청`을 보낸다.
  2) 수신측 컴퓨터에서 송신측에서 받은 요청을 허가하기 위해 `ACK요청`을 보낸다. 동시에 수신측도 송신측에 `SYN요청`을 보내 데이터 전송허가 요청을 보낸다.
  3) 송신측 컴퓨터에서 수신측 컴퓨터에 `ACK요청`을 보내 데이터 전송을 허가한다.
- 4 way handshaking
  - 통신이 끝난 이후, 연결을 끊기 위한 과정
  1) 송신측 컴퓨터는 수신측에 `FIN`요청을 보낸다.(연결을 끊기 위한 요청)
  2) 수신측 컴퓨터는 `ACK`요청을 보내 허가한다.
  3) 수신측 컴퓨터도 송신척에 `FIN`요청을 보낸다.
  4) 송신척 컴퓨터도 수신측에 `ACK`요청을 보내 허가한다.
#### UDP(비연결)
- 독립적인 제어 메시지를 사용하지 않는다.
- TCP헤더에 비해 간단한 헤더덕분에 통신 과부하가 적다
- 데이터 전송의 신뢰성을 보장하지 않는다
- 전송속도가 빠르다

### 세션계층(5계층)

---
### 웹사이트에 접속할때, 일어나는 데이터 처리 과정
### 구조
클라이언트 -> 스위치A -> 라우터A -> 라우터B -> 스위치B ->웹 서버
### 클라이언트가 웹서버에 요청하는 과정
0. 3-way 핸드셰이크
1. 웹사이트 url을 입력한다.
2. `응용계층`에서 `http`메세지를 보낸다.ex) GET/index.html HTTP/1.1~
3. `전송계층`에서 `TCP`헤더(출발지 포트번호(1025 이상의 값중 무작위로), 목적지 포트번호(80))를 더해 데이터를 `세그먼트`로 만든다.
4. `네트워크계층`에서 `ip`헤더(출발지IP, 목적지 IP)를 더하여 `IP패킷`을 만든다.
5. `데이터링크계층`에서 `이너넷`헤더(출발지MAC주소, 목적지MAC주소)를 데이터에 더해 `이더넷`프레임으로 만든다.
6. `물리계층`에서 데이터를 전기 신호로 변환하여, 네트워크로 전송한다.
  

7. `스위치(A)`의 물리계층 -> 데이터링크계층 -> 물리계층을 거쳐, `라우터(A)`에게 전송한다.
8. `라우터(A)`의 물리계층 -> 데이터링크계층(이더넷 프레임을 분석하여, 목적지MAC주소가 자신의 MAC과 동일하면 역캡슐화를 수행한다.) -> 네트워크 계층(라우팅 테이블과 목적지 IP주소를 비교후 라우팅) -> 데이터링크계층- > 물리계층 을 통해 `라우팅`된 주소로 전달한다.  
  

9. `라우터(B)`의 물리계층 -> 데이터링크계층(목적지MAC주소가 같으면 역캡슐화 수행) -> 네트워크계층(자신의IP와 목적지IP주소를 비교한후 라우팅) -> 데이터링크계층 -> 물리 계층
10. `스위치(B)`의 물리계층 -> 데이터링크계층 -> 물리계층을 통해 웹서버로 전달함.
  

11. `웹서버`의 물리계층 -> 데이터링크계층(자신의 MAC주소와, 목적지MAC주소를 비교한 뒤 일치하면 이너뎃헤더, 트레일러를 분리함.) -> 네트워크계층(목적지IP와 웹서버 자신의 IP주소가 같은지 확인한뒤 일치하면 IP헤더를 분리함) -> 전송계층(목적지 포트번호를 확인하여 어떤 어플리케이션으로 전달해야하는지 판단한 뒤 TCP헤더를 분리함) -> 응용계층
12. 위 과정을 역순으로 웹서버가 클라이언트에 응답함.