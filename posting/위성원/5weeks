# 4장 스위치
## 4.1 스위치 장비 동작
 - 스위치는 네트워크에서 통신을 중재
 - 스위치의 핵심 역할은 단말이 어느 위치에 있는지 파악하고 해당 위치로 패킷을 정확히 전송하는 것.
 - MAC 주소 테이블을 통해 단말의 주소인 MAC주소와 단말이 위치하는 인터페이스 정보를 알고있어 위와같은 통신이 가능함.
 ![image-20211121183011770](C:\Users\tkrhk\AppData\Roaming\Typora\typora-user-images\image-20211121183011770.png)
 - 스위치는 전송하려는 패킷의 헤더 안에 있는 2계층 목적지 주소를 확인.
 - MAC 주소 테이블에서 해당 주소가 어느 포트에 있는지 확인해 해당 패킷을 그 포트로만 전송한다(필터링).
 - 만약 테이블에 없는 도착지 주소를 가진 패킷이 스위치로 들어오면 스위치는 전체 포트로 패킷을 전송한다(플러딩).
 - 스위치의 동작 방식은 플러딩, 어드레스 러닝, 포워딩/필터링 3가지로 정리할 수 있음.
 ![image-20211121183307441](C:\Users\tkrhk\AppData\Roaming\Typora\typora-user-images\image-20211121183307441.png)
 ### 4.1.1 플러딩 
  - 스위치는 부팅하면 네트워크 정보가 아무 것도 없음. 이때는 허브 처럼 동작 (패킷이 들어온 포트를 제외한 모든 포트로 전달)
  - 스위치가 허브와 같이 모든 포트로 패킷을 흘리는 동작 방식을 플러딩이라고함.
  ![image-20211121183429652](C:\Users\tkrhk\AppData\Roaming\Typora\typora-user-images\image-20211121183429652.png)
  - 스위치는 LAN에서 동작하므로 자신이 정보를 갖고 있지 않더라도 어딘가에 장비가 있을 수 있다고 가정하고 위와 같이 작업을 수행.
  ![image-20211121183536605](C:\Users\tkrhk\AppData\Roaming\Typora\typora-user-images\image-20211121183536605.png)
 ### 4.1.2 어드레스 러닝
  - 스위치가 도착지의 MAC 주소를 확인하여 원하는 포트로 패킷을 전달하려면 MAC주소 테이블에 해당 정보가 있어야 한다.
  - 패킷 출발지의 MAC주소 정보를 MAC주소 테이블에 삽입하는 것을 어드레스 러닝이라 한다.
  - 패킷이 특정 포트에 들어오면 스위치에는 해당 패킷의 출발지 MAC주소와 포트 번호를 MAC주소 테이블에 기록한다.
  ![image-20211121183943135](C:\Users\tkrhk\AppData\Roaming\Typora\typora-user-images\image-20211121183943135.png)
  - 어드레스 러닝은 출발지의 MAC주소 정보를 사용하므로 브로드캐스트나 멀티캐스트에 대한 MAC주소를 학습할 수 없다. (두 가지 모두 목적지 MAC 주소만 사용함)
 ### 4.1.3 포워딩/필터링
  - 포워딩 : 스위치에 패킷이 들어온 경우, 자신의 MAC 테이블과 패킷에 있는 도착지 MAC주소를 확인하여 맞는 정보를 해당 포트로 보냄.
  - 필터링 : 포워딩할 때 목적지로만 패킷을 보내는 것.
  - 스위치에서는 포워딩과 필터링 작업이 여러포트에서 동시에 수행될 수 있음.
  - 통신이 다른 포트에 영향을 미치지 않으므로 다른 포트에서 기존 통신작업으로부터 독립적으로 동작할 수 있음.
  ![image-20211121184400071](C:\Users\tkrhk\AppData\Roaming\Typora\typora-user-images\image-20211121184400071.png)
  - 스위치는 일반적인 유니캐스트에 대해서만 포워딩과 필터링 작업을 수행함. 
  - BUM 트래픽이라고 부르는 브로드캐스트와 언노운 유니캐스트, 멀티캐스트는 조금 다르게 동작, 
  - 출발지 MAC 주소로 브로드캐스트나 멀티캐스트 모두 출발지가 사용되지 않으므로 이런 트래픽은 전달이나 필터링 작업을 하지 않고 모두 플러딩함. 
  - 언노운 유니캐스트도 MAC 주소 테이블에 없는 주소이므로 브로드캐스트와 동일하게 플러딩.
  
## 4.2 VLAN
 - 물리적 배치와 상관없이 LAN을 논리적으로 분할, 구성하는 기술.
 - 네트워크를 분할해야 하는 상황에서 스위치의 공간을 효율적으로 사용하기 위한 가상화 기술.
### 4.2.1 VLAN이란?
 ![image-20211121192009901](C:\Users\tkrhk\AppData\Roaming\Typora\typora-user-images\image-20211121192009901.png)
 - VLAN을 나누면 하나의 장비를 서로 다른 네트워크를 갖도록 분할한 것이므로 VLAN간에 통신을 할 수 없다.
 - 통신이 필요하다면 3계층 장비가 필요 (but 요즘은 LAN카드가 좋아져서 VLAN정보를 인식할 수 있음.)
 - 물리적으로 다른 층에 있는 단말이 하나의 VLAN을 사용해 동일한 네트워크로 묶일 수 있음.
 ![image-20211121192720549](C:\Users\tkrhk\AppData\Roaming\Typora\typora-user-images\image-20211121192720549.png)
### 4.2.2 VLAN의 종류와 특징
 - VLAN 할당 방식에는 포트 기반의 VLAN과 MAC주소 기반의 VLAN이 있음.
 - 포트기반 VLAN : 스위치를 논리적으로 분할해 사용함, 일반적으로 언급하는 대부분의 VLAN
 - 어떤 단말이 접속하든지 스위치의 특정 포트에 VLAN을 할당하면 할당된 VLAN에 속하게 됨.
 - MAC 기반 VLAN : 스위치의 고정 포트에 VLAN을 할당하는 것이 아닌 스위치에 연결된 단말의 MAC 주소를 기반으로 할당.
 - 단말이 연결되면 단말의 MAC 주소를 인식한 스위치가 해당 포트를 지정된 VLAN으로 변경.
 - 단말에 따라 VLAN 정보가 바뀔 수 있어 다이나믹 VLAN(Dynamic VLAN)이라고도 부름.
 ![image-20211121193118618](C:\Users\tkrhk\AppData\Roaming\Typora\typora-user-images\image-20211121193118618.png)
### 4.2.3 VLAN 모드(Trunk/Access) 동작 방식
 - 한 대의 스위치에 연결되더라도 서로 다른 VLAN이 설정된 포트 간에는 통신할 수 없음.
 - 3계층 장비를 사용해야만 서로 다른 VLAN간의 통신이 가능.
 - VLAN으로 구분된 네트워크에서는 브로드캐스트인 ARP 리퀘스트가 다른 VLAN으로 전달될 수 없으므로 3계층으로 통신해야 함.
 ![image-20211121193907705](C:\Users\tkrhk\AppData\Roaming\Typora\typora-user-images\image-20211121193907705.png)
 - VLAN을 사용하는 스위치간의 통신을 위해서는 각 VLAN 별로 스위치마다 포트를 마련해야 함
 ![image-20211121194323167](C:\Users\tkrhk\AppData\Roaming\Typora\typora-user-images\image-20211121194323167.png)
 - VLAN을 많이 사용하는 중-대형 네트워크에서는 VLAN별로 포트를 연결해야하므로 많은 포트가 낭비됨.
 ![image-20211121194416766](C:\Users\tkrhk\AppData\Roaming\Typora\typora-user-images\image-20211121194416766.png)
 - 한 개의 포트로 여러 VLAN통신이 가능한 태그 포트를 사용하여 문제 해결.
 - 태그 기능은 하나의 포트에 여러 개의 VLAN을 함께 전송할 수 있게 해줌.
 - 이 포트를 태그포트 또는 트렁크포트라고함.
 ![image-20211121194533886](C:\Users\tkrhk\AppData\Roaming\Typora\typora-user-images\image-20211121194533886.png)
 - 이런 태그 포트 기능이 스위치에 생기면서 스위치의 패킷 전송에 사용하는 MAC 주소 테이블에도 변화가 생김. 
 - 다른 VLAN끼리 통신하지 못하도록 MAC 테이블에 VLAN을 지정하는 필드가 추가된 됨. 
 - 즉, 하나의 스위치에서 VLAN을 이용해 네트워크를 분리하면 VLAN별로 MAC 주소 테이블이 존재하는 것처럼 동작함.
 ![image-20211121194724983](C:\Users\tkrhk\AppData\Roaming\Typora\typora-user-images\image-20211121194724983.png)
 

   
