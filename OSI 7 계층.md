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

## 4. Transport Layer
- 1,2,3 계층은 신호와 데이터를 올바른 위치로 보내는데 집중 -> **4 계층은 정상적으로 잘 보내지는지 확인하는 역할**
- 데이터를 분할해 패킷에 실어 보냄 -> 유실, 순서 섞이는 가능성 존재 -> **바로 잡는 역할**
- 포트 번호를 이용해 상위 Application 구별
- 장비: 로드 밸런서, 방화벽

## 5. Session Layer
- 양 끝단의 프로세스가 **연결 성립, 안정적으로 연결 유지, 작업 완료** 후 연결 종료를 담당
- 세션을 만들고 없애는 역할

## 6. Presentation Layer
- 표현 방식이 다른 application, 시스템 간의 통신을 돕기위해 하나의 통일된 구문 형식으로 변환 (번역기 같은 역할)
ex) MIME 인코딩, 암호화, 압축

## 7. Application Layer
- 어플리케이션 서비스 수행
- FTP, SMTP, HTTP, TELNET
