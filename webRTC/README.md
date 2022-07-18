## WebRTC
* WebRTC(Web Real-Time Communication)는 웹 브라우저 간에 플러그인의 도움 없이 서로 통신할 수 있도록 설계된 API이다.
  * 브라우저에서 별도의 소프트웨어 없이 비디오, 음성 및 일반 데이터가 피어간에 실시간으로 전송 가능하게 해주는 오픈 프레임워크
  * 보통 브라우저에서 실행할 때 JavaScript API를 통해 실행할 수 있어 개발자들로 하여금 쉽게 RTC web app을 실행하는 것이 가능
  * W3C와 IETF에서 API레벨과 Protocol레벨을 표준화함 

## NAT
* Network Address Translation
* 단말에 공개 IP 주소를 할당하기 위해 사용됨.
* 라우터는 공개 IP주소를 갖고 있고 모든 단말들을 라우터에 연결되어 있으며 비공개 IP 주소를 갖고 있다.
* 요청은 단말의 비공개 주소로부터 라우터의 공개 주소와 유일한 포트를 기반으로 번역됨
* 각각의 단말이 유일한 공개 IP없이 인터넷상에 검색될 수 있는 방법

## STUN
1. Session Traversal Uilities for NAT의 약자이다.
2. NAT환경에서는 Private IP를 별도로 가지고 있기 때문에 Peer to Peer 통신이 불가능하다.
3. 클라이언트는 자신의 Public IP를 확인하기 위해 STUN 서버로 요청을 보내고 서버로부터 자신의 Public IP를 받는다.
4. 클라이언트는 자신이 받은 Public IP를 이용하여 시그널링을 할 때 받은 그 정보를 이용해서 시그널링을 하게 한다.

## TURN
1. TURN 서버는 클라이언트들이 통신할 때 Public망에 존재하는 TURN서버를 경유하여 통신하게 된다.
2. 클라이언트는 자신의 Private IP가 포함된 TURN메세지를 턴서버로 보낸다
3. TRUN 서버는 메세지에 포함된 Network Layer IP주소와 Transport Layer의 UDP포트 넘버와의 차이를 확인하고 클라이언트의 Public IP로 응답한다.
4. NAT는 NAT 매핑테이블에 기록되어 있는 정보에 따라서 내부 네트워크에 있는 클라이언트의 Private IP로 메세지를 전송한다.
