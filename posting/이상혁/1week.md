# 1장 : 네트워크 시작하기

- [인터넷 네트워크](#인터넷-네트워크)
  - [인터넷 네트워크의 구성](#인터넷-네트워크-구성)
  - [Home/Enterprise Network](#Home/Enterprise-Network)
- [프로토콜](#프로토콜)
- [OSI 7계층과 TCP/IP 모델](#OSI-7계층과-TCP/IP-모델)
  - [OSI 7 Layer](#OSI-7-Layer)
  - [TCP/IP Model](#TCP/UP-Model)
  - [인터넷 네트워크를 계층화하여 나눈 이유](#인터넷-네트워크를-계층화하여-나눈-이유)

## 인터넷 네트워크
- 네트워크에는 다양한 네트워크들이 있지만, 여기서는 가장 규모가 크고 유명한 인터넷 네트워크를 대상으로 한다.

### 인터넷 네트워크 구성
- 인터넷 네트워크는 크게 코어, 엣지, 액세스 링크 부분으로 볼 수 있다.
- 네트워크 엣지
  - 네트워크의 가장 끝 점 (엔드시스템)
  - 애플리케이제션 프로그램을 호스팅하고 잇기 때문에 호스트라고 한다.
  - 클라이언트의 애플리케이션 메세지를 받고, 이것을 패킷으로 불리는 조각으로 나눈다음 access network로 연결되는 링크로 밀어넣는다.
- 네트워크 코어
  - 라우터/스위치들이 여기에 속함
  - end system들 간의 데이터를 전달해주는 것이 목적
  - 데이터 전송 방식
    - circuit switching
      - 전화연결에 주로 사용
      - call set up : 두 엔드시스템 간의 데이터 전송 이전에 서로 경로를 설정하고 자원을 예약해둔다. (resource reservation이 발생)
      - 장점 : no sharing
      - 단점 : 두 시스템을 독립적으로 연결해놔야하기 때문에 네트워크 자원을 분할해놔야 함 (FDM/TDM 방식으로 분할)
      - 전화 네트워크에 유리/인터넷 네트워크에 불리
    - packet switching
      - no resource reservation : 자원 예약이 필요하지 않음, 필요가 발생하면 그때그때 전체 링크 full capacity를 할당해준다.
      - break app messages into packet : 만약, 한 유저 데이터가 굉장히 크다면 별다른 조치를 취하지않는한 그 데이터가 링크를 독점하게 된다. 이를 방지하기 위해서 패킷 스위칭 방식에서는 유저 데이터를 작은 packet으로 조각내서 전송한다. 패킷의 크기를 일정하게하면 각 유저 데이터가 링크를 점유하는 시간이 고정적으로 될 수 있다.
      - store and forward : 서킷 방식에서는 call-setup이 일어나므로 두 엔드시스템 간의 경로가 이미 설정되어있다. 하지만, 패킷 방식에서는 그렇지 못하므로 패킷에다가 목적지 주소를 넣어줘야한다. 따라서, 서킷 방식에서는 데이터가 파이프에 물을 흘려보내듯이 전송될 수 있지만 패킷 방식에서는 목적지 주소를 반드시 봐야하기 때문에 각 홉에서는 하나의 패킷이 모두 다 올때까지 받는 작업만 한 후 다 받은다음에서야 전송할 수 있다.  
        - queueing delay & loss (congestion) : 패킷 방식이 store & forward 이기 때문에, 라우터에서는 버퍼를 두는데 패킷을 내보내는 속도보다 들어오는 속도가 빨라지면 queueing delay가 발생하고 버퍼가 넘치면 packet loss가 발생한다.
      - 자원 공유 측면에서는 훌륭하지만, delay가 중요한 streaming service 에서는 치명적임 (프레임 간의 간격이 확보되어야함)
  - network of networks 
    - 인터넷은 하나의 작은 네트워크들이 다른 더 큰 네트워크에 연결되고 다시 이 큰 네트워크가 더 큰 네트워크에 연결되는 계층적인 구조이다.
- 액세스 네트워크 (Access Network)
  - 엔드시스템들을 인터넷으로 연결해줌
  - Bandwidth : 일반적으로 데이터 전송 속도 bps
  - 크게 shared/dedicated 링크로 나뉜다.
  - 액세스 네트워크의 종류
    - DSL (Digital Subscriber line)
      - 전화회사에서 제공해주는 액세스 네트워크
      - dedicated line
      - 인터넷(모뎀), 집 전화기가 다 전화회사에 연결되어 있고, 이 전화회사의 센트럴 오피스에 중앙 멀티플렉스가 있어서 이게 전화연결이면 전회 네트워크로 보내고 인터넷 연결이면 인터넷 네트워크로 보낸다.
    - Cable
      - 케이블 회사를 통해서 인터넷에 연결하는 경우 케이블을 모뎀을 통해서 인터넷에 연결
      - shared line
      - 일반적으로 케이블 방송은 broadcast 해야하기 때문에 중앙에 큰 링크를 두고 shared 하는 방식
        - 전화는 집집마다 연결되는 시간이 다르기 때문에 dedicated, TV와 같이 방송은 같은 시간대에 같은 데이터를 보내기 때문에 shared
      - HFC라고도 한다. (coax, fiber 링크의 조합으로 이루어져 있음)
    - wireless access network
      - wireless LANs (wifi) : wifi는 wifi access point에 연결이 되고 이것은 다시 더 큰 이더넷 스위치에 연결이 되고 이것은 다시 더 큰 라우터에 연결이 된다. 이 라우터는 다시 집이라면 케이블/전화 회사에 연결되고 학교/기관이라면 독립적인 dedicated line으로 곧 바로 ISP 네트워크에 연결된다.
      - wide-area wireless access (3G, LTE, ...) : 셀룰러 네트워크라고도 한다.
      - wifi는 좁은 범위(LAN)이지만 대역폭이 매우 높고 셀룰러 네트워크는 광범위 (WAN)이지만 와이파이에 비해 대역폭이 낮다. 공통점은 둘 다 shared, wireless 이다.
  - guided media
    - copper(ethernet), HFC(fiber, coax)
    - twisted pair (copper) : ethernet에서 사용
    - coaxial cable : tp보다 더 대역폭이 큼, HFC에서 사용
    - fiber optic cable : light purse이므로 멀리가더라도 주변 노이즈에 영향을 받지 않으며 매우 빠름, 대륙간에 연결
  - unguided media
    - radio(wifi, cellular) : 전기신호
      - 물리적인 선이 없음, 장애물에 취약, 전자기장이므로 주변 노이즈에 매우 취약
      - terrestrial microwave, LAN, wide-area, satellite 등이 있음

### Home/Enterprise Network
- Home Network
  - 우리 집에는 데스크탑, 스마트폰 등 여러 개의 엔드시스템이 존재하는데 이것들이 하나의 독립적인 작은 로컬 네트워크를 구성한다.
  - 이 Home Network가 전화/케이블 네트워크로 연결되고, 전화/케이블 회사에서 다시 인터넷 세상으로 연결된다.
  - 홈 네트워크의 코어에는 라우터(공유기)가 있는데, 일반적으로 이 라우터에 데스크탑은 직접 물려있고(유선으로) 스마트폰은 wifi access point에 연결되어있다.
  - 즉, 이 라우터가 홈 네트워크 안의 엔드시스템들을 묶어서 전화/케이블 회사에 연결해준다.
- Enterprise Access Networks (Ethernet)
  - 학교/회사/기관 같은 곳은 엔드시스템들이 훨씬 많기 때문에 앞서 본 홈 네트워크 처럼 연결되지는 않는다.
  - 한 건물/층/방 안에 있는 엔드시스템들은 이더넷 스위치에 연결되고 wifi access point도 이더넷 스위치에 물린다.
  - 이 이더넷 스위치들은 다시 학교 전체 혹은 건물 전체를 연결해주는 라우터로 연결되고 라우터는 다시 ISP에 연결된다.
  - 홈 네트워크는 전화/케이블 회사가 직접 ISP 네트워크에 연결해주지만(shared) 학교/기관 네트워크는 규모가 다르기 때문에 이들을 엮어주는 라우터가 ISP에게 연결되고 이 ISP에서 dedicated line으로 인터넷에 연결해준다.
  - 이 dedicated line은 케이블/전화회사가 아니라 ISP가 직접 구성하여 연결해준다.

## 프로토콜
- 프로토콜에 대한 설명 (표준화가 매우 중요 오픈되어야함, 프로토콜에서 정의하고 있는 것)
- 인터넷 네트워크에서 사용하는 많은 프로토콜들
- 인터넷 상에서 메세지(데이터)를 주고받기 위해 표준화되고 오픈된 표준안이 필요

## OSI 7계층과 TCP/IP 모델

### OSI 7 Layer
- 과거 네트워크가 표준화되지 않던 시절 이를 하나로 통합하기 위해 나타남
- 현재는 OSI 7 계층은 주로 레퍼런스 모델로 사용되며 보다 현실적이고 실용적인 TCP/IP 모델이 주로 사용
- OSI 7 계층은 크게 2가지로 나눌 수 있다.
  - Application Layer / Upper Layer
    - `Application - Presentation - Session` 계층이 속함 
    - 데이터가 어떻게 전달되는지 고려하지 않고, 데이터를 어떻게 표현하는지에 집중
    - 애플리케이션 개발자 중심
  - Data flow Layer / Lower Layer
    - `Physical - Link - Network - Transport` 계층이 속함
    - 데이터가 어떻게 표현되는지 신경쓰지 않고, 데이터를 어떻게 잘 전달하는지에 집중
    - 네트워크 엔지니어 중심

### TCP/IP Model
- 

### 인터넷 네트워크를 계층화하여 나눈 이유
- 복잡한 네트워크 세상을 각 역할에 따라 추상화함으로써 네트워크 참여자들은 상위, 하위 계층에서 일어나는 일을 신경쓰지 않고 자신이 속한 계층에만 집중할 수 있음
- 계층을 나누었기 때문에 역할과 책임을 명확히 할 수 있음

- 책 2장/3.1 내용 추가
-
가