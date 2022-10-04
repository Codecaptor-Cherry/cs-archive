# TCP/IP 그리고 UDP

# TCP/IP란

TCP/IP 는 가장최근에 발명된 **컴퓨터와 컴퓨터**
간의 지역네트워크(LAN) 혹은 광역네트워크(WAN)에서 원할한 통신을 가능하도록 하기 위한 통신규약(Protocol) 으로 정의할 수 있다.TCP/IP 는 TCP와 IP의 2개의 프로토콜로 이루어져 있는데, 통상 IP 프로토콜 위에 TCP 프로토콜이 놓이게 되므로 TCP/IP 라고 부르게 되었다.

올바른 통신을 위해 TCP가 가지고 있는 기능

1. 패킷이 빠졌을경우, 재전송을 요청하는 기능
2. 패킷에 일련번호를 줌으로써, 서로 다르게 도착될지도 모르는 패킷의 순서를 재조합하는 기능

# TCP

## TCP

TCP의 흐름제어와 혼잡제어에 관한 더 자세한글(슬라이딩 윈도우)

[TCP/IP (흐름제어/혼잡제어) | 👨🏻‍💻 Tech Interview](https://gyoogle.dev/blog/computer-science/network/%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4%20&%20%ED%98%BC%EC%9E%A1%EC%A0%9C%EC%96%B4.html)

### TCP의 특징

- 연결형 서비스로 가상 회선 방식을 제공한다.
- 3-way handshaking과정을 통해 연결을 설정하고 4-way handshaking을 통해 해제한다.
- 흐름 제어 및 혼잡 제어.높은 신뢰성을 보장한다.
- UDP보다 속도가 느리다.전이중(Full-Duplex), 점대점(Point to Point) 방식.
- 서버소켓은 연결만을 담당한다.
- 연결과정에서 반환된 클라이언트 소켓은 데이터의 송수신에 사용된다형 서비스로 가상 회선 방식을 제공한다.
- 서버와 클라이언트는 1대1로 연결된다.
- 스트림 전송으로 전송 데이터의 크기가 무제한이다.
- 패킷에 대한 응답을 해야하기 때문에(시간 지연, CPU 소모) 성능이 낮다.
- Streaming 서비스에 불리하다.(손실된 경우 재전송 요청을 하므로)

이러한 특징들 때문에 신뢰성을 요구하는 파일전송 같은 경우에 사용된다.

### 3way handshake - 연결시

![Untitled](TCP%20IP%20%E1%84%80%E1%85%B3%E1%84%85%E1%85%B5%E1%84%80%E1%85%A9%20UDP%207c3062a3d44b4123a272faaf4a00cdbd/Untitled.png)

1. 클라이언트가 서버에게 SYN 패킷을 보냄 (sequence : x)
2. 서버가 SYN(x)을 받고, 클라이언트로 받았다는 신호인 ACK와 SYN 패킷을 보냄 (sequence : y, ACK : x + 1)
3. 클라이언트는 서버의 응답은 ACK(x+1)와 SYN(y) 패킷을 받고, ACK(y+1)를 서버로 보냄

### 4way handshake - 연결해제

![Untitled](TCP%20IP%20%E1%84%80%E1%85%B3%E1%84%85%E1%85%B5%E1%84%80%E1%85%A9%20UDP%207c3062a3d44b4123a272faaf4a00cdbd/Untitled%201.png)

1. 클라이언트는 서버에게 연결을 종료한다는 FIN 플래그를 보낸다.
2. 서버는 FIN을 받고, 확인했다는 ACK를 클라이언트에게 보낸다. (이때 모든 데이터를 보내기 위해 CLOSE_WAIT 상태가 된다)
3. 데이터를 모두 보냈다면, 연결이 종료되었다는 FIN 플래그를 클라이언트에게 보낸다.
4. 클라이언트는 FIN을 받고, 확인했다는 ACK를 서버에게 보낸다. (아직 서버로부터 받지 못한 데이터가 있을 수 있으므로 TIME_WAIT을 통해 기다린다.)
- 서버는 ACK를 받은 이후 소켓을 닫는다 (Closed)
- TIME_WAIT 시간이 끝나면 클라이언트도 닫는다 (Closed)

여기서 TIME-WAIT등은 TCP state에 해당된다.

### TCP state

**LISTEN :**

서버의 데몬이 떠서 접속 요청을 기다리는 상태

**SYN-SENT :**

로컬의 클라이언트 어플리케이션이 원격 호스트에 연결을 요청한 상태

**SYN_RECEIVED :**

서버가 원격 클라이언트로부터 접속 요구를 받아 클라이언트에게 응답을 하였지만 아직 클라이언트에게 확인 메시지는 받지 않은 상태

**ESTABLISHED :**

3 way-handshaking 이 완료된 후 서로 연결된 상태

**FIN-WAIT1, CLOSE-WAIT, FIN-WAIT2 :**

서버에서 연결을 종료하기 위해 클라이언트에게 종결을 요청하고 회신을 받아 종료하는 과정의 상태

**TIME-WAIT :**

연결은 종료되었지만 분실되었을지 모를 느린 세그먼트를 위해 당분간 소켓을 열어두고 있는 상태

**CLOSING :**

흔하지 않지만 주로 확인 메시지가 전송도중 분실된 상태

**CLOSED :**

완전히 종료

### TCP 헤더정보

![Untitled](TCP%20IP%20%E1%84%80%E1%85%B3%E1%84%85%E1%85%B5%E1%84%80%E1%85%A9%20UDP%207c3062a3d44b4123a272faaf4a00cdbd/Untitled%202.png)

| --- | --- | --- |

# UDP

### UDP 주요 특징

- 비연결형 서비스로 데이터그램 방식을 제공한다정보를 주고 받을 때 정보를 보내거나 받는다는 신호절차를 거치지 않는다.
- UDP헤더의 CheckSum 필드를 통해 최소한의 오류만 검출한다.
- 신뢰성이 낮다
- TCP보다 속도가 빠르다(스트리밍 서비스에 주로 사용)

# TCP 와 UDP

![Untitled](TCP%20IP%20%E1%84%80%E1%85%B3%E1%84%85%E1%85%B5%E1%84%80%E1%85%A9%20UDP%207c3062a3d44b4123a272faaf4a00cdbd/Untitled%203.png)

![Untitled](TCP%20IP%20%E1%84%80%E1%85%B3%E1%84%85%E1%85%B5%E1%84%80%E1%85%A9%20UDP%207c3062a3d44b4123a272faaf4a00cdbd/Untitled%204.png)

# IP

TCP와 달리 UDP는 비연결형 프로토콜이다. 즉 연결을 위해 할당되는 논리적인 경로가 없는데, 그렇기 때문에 다른 경로로 전송되고 독립적으로 처리하게된다.

# 참고링크

[[TCP] 3 way handshake & 4 way handshake | 👨🏻‍💻 Tech Interview](https://gyoogle.dev/blog/computer-science/network/TCP%203%20way%20handshake%20&%204%20way%20handshake.html)

[TCP/IP 쉽게 이해하기](https://aws-hyoh.tistory.com/entry/TCPIP-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)

[네트워크 프로그래밍 : TCP/IP 개론](https://www.joinc.co.kr/w/Site/Network_Programing/Documents/IntroTCPIP)

[TCP/IP(Transmission Control Protocol/Internet Protocol)](https://www.ibm.com/docs/ko/aix/7.1?topic=management-transmission-control-protocolinternet-protocol)

데이터 전송의 과정에서 TCP와 IP 각각 담당하는 작업이 있지만, 결국에는 같은 결과를 목표로 하기 때문에 한 명칭으로 알려지기도 한다.