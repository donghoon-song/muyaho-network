# OSI 7 계층
네트워크에서 통신이 일어나는 과정을 7단계로 나눔

## OSI 7계층을 나눈 이유?
통신이 일어나는 과정을 단계별로 파악할 수 있어 트러블슈팅에 유리

## OSI 7 계층 단계
![image](https://user-images.githubusercontent.com/32301380/114417762-d4d13680-9bec-11eb-8f93-5a80a335efc8.png)

|계층|이름|PDU|
|:--:|:--:|:--:|
|7|	Application Layer|Data|
|6|	Presentation Layer|Data|
|5|	Session Layer|Data|
|4|	Transport Layer|Segment|
|3|	Network Layer|Packets|
|2|	Data Link Layer|Frames|
|1|	Physical Layer|Bits|

- PDU (Protocol Data Unit)
- 7~5 계층은 **Application Layer**이라 부르고 데이터 표현에 초점을 둔다
- 4~1 계층은 **Data flow layer**라고 부르고 데이터를 상대방에게 전달하는 역할을 한다

## 1. Physical Layer
- 물리적인 연결
- `데이터를 전달만`할 뿐, 데이터가 무엇인지 어떤 에러가 있는지 신경쓰지 않음
- 주소 : 개념이 없음 -> 신호가 들어온 포트를 제외하고 모든 포트에 전기 신호를 전송한다
- 장비 : Hub, Repeater, Cable, Connector, Tranceiver, TAP

## 2. Data Link
- 정보의 오류와 흐름을 관리
- 전기 신호를 데이터로 변환
- 주소 : **MAC 주소**
- 출발, 도착 MAC 주소를 확인, 에러 탐지, 재전송 등의 기능
- 데이터를 받는 사람이 현재 데이터를 받을 수 있는지 확인하는 작업을 수행 -> **flow control**
- 장비 : 네트워크 인터페이스 카드(NIC) -> 랜카드도 여기에 포함됨, 스위치

### 스위치
- 1계층 Physical Layer에서는 한 포트에서 입력이 들어오면 전체 포트로 전기신호를 전달했다. -> 동시에 한 장비만 데이터 전송 가능하다는 의미
- 하지만, 스위치는 통신이 필요한 포트만 사용 -> 네트워크 전체에 불필요한 처리 감소 -> 이더넷 효율 높아짐

### Network Interface Card의 동작 예시
1. 전기 신호 -> 데이터
2. 목적지 MAC 주소,  출발지 MAC 주소 확인
3. Network Interface Card의 MAC 주소 확인
4. 목적지 MAC과 NIC MAC 주소가 같으면 처리. (다르면 폐기)

## 3.  Network Layer
- 데이터를 목적지까지 가장 안전하고 빠르게 전달
- 주소: IP와 같은 논리적인 주소
- 장비: 라우터 (IP 주소를 이해할 수 있고, 최적의 경로를 찾아 해당 경로로 패킷 전송)
- 3계층 장비들은 자신이 속한 네트워크, 원격지 네트워크를 구분할 수 있고, 경로를 지정할 수 있다.

### IP 계층
- TCP/IP상에서 IP 패킷의 전달 및 라우팅을 담당
- 하위 계층인 데이터링크 계층의 하드웨어적인 특성에 관계없이 `독립수행`

### IP 프로토콜
- 데이터그램의 전달을 담당
- IP 계층에서 IP 패킷의 라우팅 대상이 됨(Routing)
- IP 주소 지정(Addressing)
- 신뢰성(에러제어) 및 흐름제어 기능이 전혀 없음 -> Best-Effort Service
  - 신뢰성을 확보하려면 IP계층 위의 TCP와 같은 상위 트랜스포트 계층에 의존
- 비연결성 데이터그램 방식 -> Connectionless
- 패킷의 완전한 전달(소실, 중복, 지연, 순서바뀜 등이 없게함)을 보장하지 않음 -> Unreliable
- IP패킷 헤더 내 수신 및 발신 주소 포함 -> IPv4헤더, IPv6헤더, IP주소
- IP 단편화가 필요
- TCP, UDP, ICMP, IGMP 등이 IP 데이터그램에 실려 전송

## 4. Transport Layer
- 통신을 활성화하기 위한 계층
- 1,2,3 계층은 신호와 데이터를 올바른 위치로 보내는데 집중 -> **4 계층은 정상적으로 잘 보내지는지 확인하는 역할**
- 패킷들의 전송이 유효한지 확인하고 전송 실패한 패킷들을 다시 전송
- 데이터를 분할해 패킷에 실어 보냄 -> 유실, 순서 섞이는 가능성 존재 -> **바로 잡는 역할**
- 포트 번호를 이용해 상위 Application 구별
- 양 끝단 사용자들이 신뢰성있는 데이터를 주고받을 수 있도록 보장
- 상위 계층들이 데이터 전달의 유효성이나 효율성을 생각하지 않도록 도와줌
- 연결 기반(connection oriented)
- 장비: 로드 밸런서, 방화벽

## TCP 프로토콜(Transmission Control Protocol)
OSI 계층 모델에서 전송 계층(4계층)에 해당
1. 신뢰성(Reliable)
  - 패킷 손실, 중복, 순서바뀜 등이 없도록 보장
  - TCP 하위계층인 IP 계층의 신뢰성 없는 서비스에 대해 다방면으로 신뢰성을 제공
2. 연결지향적(Connection-oriented)
  - 느슨한 연결(Loosely Connected)
  - 연결 관리를 위한 설정 및 해제 필요 (TCP 연결 설정, 연결 종료)
  - 양단간 어플리케이션/프로세스는 TCP가 제공하는 연결성 회선을 통해 서로 통신
  - 연결 시 3-way handshaking, 종료 시 4-way handshaking

## UDP 프로토콜(User Datagram Protocol)
신뢰성이 낮은 프로토콜(완정성 보장 X)
1. `비연결성`, `신뢰성 X`, 순서화되지 않은 Datagram 서비스 제공
  - 메시지가 제대로 도착했는지 확인 X (`확인응답 X`)
  - 수신된 메시지의 순서를 맞추지 않음 (`순서제어 X`)
  - 흐름 제어를 위한 피드백 제공 X (`흐름제어 X`)
  - UDP를 사용하는 프로그램 쪽에서 오류제어 기능을 스스로 갖추어야 함
  - 데이터그램 지향의 전송계층용 프로토콜(`논리적인 가상회선 연결 필요 X`)
2. `실시간 응용 및 멀티캐스팅` 가능
  - `빠른 요청과 응답`이 필요한 실시간 응용에 적합
  - 여러 다수 지점에 전송 가능 (1대다)
3. `헤더가 단순`
  - UDP는 TCP처럼 16비트의 포트 번호를 사용하나 헤더는 고정크기의 8바이트(TCP는 20바이트)만 사용
  - 즉, 헤더 처리에 많은 시간과 노력 X

## 5. Session Layer
- 양 끝단의 프로세스가 **연결 성립, 안정적으로 연결 유지, 작업 완료** 후 연결 종료를 담당
- 세션을 만들고 없애는 역할
- 동시 송수신 방식(duplex), 반이중 방식(half-duplex), 전이중 방식(Full duplex), 체크 포인팅, 유휴, 종료, 다시 시작 과정 수행
- RPC, Socket

## 6. Presentation Layer
- 표현 방식이 다른 application, 시스템 간의 통신을 돕기위해 하나의 통일된 구문 형식으로 변환 (번역기 같은 역할)
- 사용자 시스템에서 데이터의 형식상 차이를 다루는 부담을 응용 계층으로부터 덜어준다.
ex) MIME 인코딩, 암호화, 압축

## 7. Application Layer
- 어플리케이션 서비스 수행
- HTTP, FTP, SMTP, POP3, IMAP, Telnet
- 모든 통신의 양 끝단이다. 해당 통신 패킷들이 위의 프로토콜에 의해 모두 처리
