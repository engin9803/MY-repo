## - TCP와 UDP 차이점

- TCP(Transmission Control Protocol)/IP(Internet Protocol)  
    - IP (Internet Protocol)  
        - 패킷 전달 여부를 보증하지 않고, 패킷을 보낸 순서와 받는 순서가 다를 수 있다
        - 패킷(Packet)이란?  
        인터넷 내에서 데이터를 보내기 위한 경로배정(라우팅)을 효율적으로 하기 위해서 데이터를 여러 개의 조각들로 나누어 전송을 하는데 이때, 이 조각을 패킷이라고 한다
    - TCP (Transmission Control Protocol)  
        - IP 위에서 동작하는 프로토콜로, 데이터의 전달을 보증하고 보낸 순서대로 받게 해준다 

- [ TCP 특징 ]연결형 서비스로 가상 회선 방식을 제공한다.  
    - 3-way handshaking과정을 통해 연결을 설정하고 4-way handshaking을 통해 해제한다.
    - 흐름 제어 및 혼잡 제어
    - 높은 신뢰성을 보장 (3-way handshaking과정으로 인해)
    - UDP보다 속도가 느리다. (CPU를 사용하기 때문에 속도에 영향을 줌)
    - 전이중(Full-Duplex), 점대점(Point to Point) 방식

- [ TCP 서버의 특징 ]  
    - 서버소켓은 연결만을 담당한다.
    - 연결과정에서 반환된 클라이언트 소켓은 데이터의 송수신에 사용된다형 서비스로 가상 회선 방식을 제공
    - 서버와 클라이언트는 1대1로 연결  
    - 스트림 전송으로 전송 데이터의 크기가 무제한
    - 패킷에 대한 응답을 해야하기 때문에(시간 지연, CPU 소모) 성능이 낮다
    - 스트리밍(Streaming) 서비스에 불리하다.(손실된 경우 재전송 요청을 하므로)

 - UDP(User Datagram Protocol)  
    - UDP는 비연결형 서비스이며 연결을 설정하고 해제하는 과정이 존재하지 않는다  
    서로 다른 경로로 독립적으로 처리함에도 패킷에 순서를 부여하여 재조립을 하거나 흐름 제어 또는 혼잡 제어와 같은 기능도 처리하지 않기에  
    TCP보다 속도가 빠르며 네트워크 부하가 적다는 장점이 있지만 신뢰성있는 데이터의 전송을 보장하지 못한다.

 - [ UDP 특징 ]
    - 비연결형 서비스로 데이터그램 방식을 제공
    - 정보를 주고 받을 때 정보를 보내거나 받는다는 신호절차를 거치지 않는다
    - UDP헤더의 CheckSum 필드를 통해 최소한의 오류만 검출
    - 신뢰성이 낮다 TCP보다 속도가 빠르다

- [ UDP 서버의 특징 ]
    - UDP에는 연결 자체가 없어서(connect 함수 불필요) 서버 소켓과 클라이언트 소켓의 구분이 없다
    - 소켓 대신 IP를 기반으로 데이터를 전송
    - 서버와 클라이언트는 1대1, 1대N, N대M 등으로 연결될 수 있다
    - 데이터그램(메세지) 단위로 전송되며 그 크기는 65535바이트로, 크기가 초과하면 잘라서 보낸다
    - 흐름제어(flow control)가 없어서 패킷이 제대로 전송되었는지, 오류가 없는지 확인할 수 없다
    - 파일 전송과 같은 신뢰성이 필요한 서비스보다 성능이 중요시 되는 경우에 사용된다  
    ex) 시간 스트리밍(streaming)

- 흐름제어(Flow Control)와 혼잡제어(Congestion Control)이란?
    - 흐름제어는
        - 데이터를 송신하는 곳과 수신하는 곳의 데이터 처리 속도를 조절하여 수신자의 버퍼 오버플로우를 방지 송신하는 곳에서 감당이 안되게 데이터를 빠르게 많이 보내면 수신자에서 문제가 발생하기 때문
    - 혼잡제어는  
        - 네트워크 내의 패킷 수가 넘치게 증가하지 않도록 방지  
        - 정보의 소통량이 과다하면 패킷을 조금만 전송하여 혼잡 붕괴 현상이 일어나는 것을 막는다

## - 요약

- TCP란?
    - 서버와 클라이언트간 신뢰성 있는 데이터 송수신을 위해 만들어진 프로토콜
    - 연결 지향성 프로토콜
    - 데이터를 나눠서 보낼수 있으며, 데이터를 받는쪽에서 나눠 받은 데이터를 재조립
    만약 누락된 데이터가 존재하면 다시 요청해서 받아와 완전한 데이터를 만든다
    - TCP로 서버/클라이언트간 연결이 된 경우 데이터를 양방향으로 주고 받을수 있다
    - 데이터의 순서가 뒤바뀌는 일 없이 안정적이라 신뢰가 가능
    - UDP에 비해 데이터 송수신 비용(부담)이 크다는 특성을 가짐
    - UDP보다 전송 속도가 느리다.

- UDP란?
    - TCP와 다르게 비연결성 프로토콜
    - 데이터를 보내고 제대로 받았는지 확인하지 않아, 데이터가 제대로 도착했는지 보장하지 않는 신뢰도가 비교적 낮다
    - 데이터를 순차적으로 보내도 받는 쪽에서는 다른 순서로 전달받을 수 있다
    - 데이터를 보내기만 하고 별 다른 처리를 하지 않기 때문에 TCP에 비해 비용(부담)이 적다는 특성을 가진다
    - TCP보다 전송 속도가 빠르다