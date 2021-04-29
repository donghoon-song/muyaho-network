# MAC(Media Access Control) 주소
Data link layer(2계층)에서 통신을 위해 네트워크 인터페이스에 할당한 고유 식별자

- 하드웨어에 고정되어 출하해서 **변경이 불가능하다**
- 제조업체가 자신의 주소 풀 안에서 할당 (주소 풀은 IEEE가 관리)

## MAC주소 구성
![](https://1.bp.blogspot.com/-BsoOnfmH4qw/WSKdrBLy0qI/AAAAAAAABNc/9zkv6Z2v14IpA7mP0hYD-yE-3stAnW4ZQCLcB/s640/Mac%2BAddress.png)
- OUI : IEEE가 제조업체에 할당해준 코드
- UAA : 제조사가 할당한 주소
- 24bit씩 총 48bit로 구성되어있다.
  
## MAC 주소 변경
- HW에 고정된 MAC 주소의 변경은 어렵다
- 하지만 MAC 주소도 메모리에 load되어 동작한다 → 변경해서 사용가능

## MAC 주소 동작
- NIC는 들어온 전기신호를 패킷으로 변환한다
- MAC 주소가 일치하거나 broadcast, multicast 그룹인 경우 → 상위 계층으로 전달한다

## 무차별모드 (promiscucous mode)
네트워크 상태 모니터링, 디버깅, 분석을 하고싶다. 하지만 NIC가 다른 목적지 패킷을 버리면 정확한 분석을 할 수 없다.

**자신의 MAC 주소가 아니어도 받도록 할 수 있다.** 
- ex) 와이어샤크
