연결 지향형 서비스


**애플리케이션 계층 메시지를 전송하기 전에 TCP는 클라이언트와 서버가 서로 전송 제어 정보를 교환하게 한다.**

이 `핸드 셰이킹(handshaking) 과정`이 클라이언트와 서버에 패킷이 곧 도달할테니 준비하라고 알려주는 역할을 한다.

  

핸드셰이킹 단계를 지나면, TCP 연결이 두 프로세스의 소켓 사이에 존재한다고 말한다.

이 연결은 두 프로세스가 서로에게 동시에 메시지를 보낼 수 있기에 `전이중 연결`이라고 한다. (3장에서 더 자세히 다룬다.)

  

### [신뢰적인 데이터 전송 서비스](https://github.com/IT-Book-Organization/Computer-Networking_A-Top-Down-Approach/tree/main/Chapter_2/2.1%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98%EC%9D%98%20%EC%9B%90%EB%A6%AC#%EC%8B%A0%EB%A2%B0%EC%A0%81%EC%9D%B8-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A0%84%EC%86%A1-%EC%84%9C%EB%B9%84%EC%8A%A4)

통신 프로세스는 **모든 데이터를 오류 없이 올바른 순서로 전달하기 위해** TCP에 의존한다.

TCP는 애플리케이션의 한 쪽이 바이트 스트림을 소켓으로 전달하면, 그 바이트 스트림이 손실되거나 중복되지 않게 수신 소켓으로 전달한다.

  

### [혼잡 제어 방식](https://github.com/IT-Book-Organization/Computer-Networking_A-Top-Down-Approach/tree/main/Chapter_2/2.1%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98%EC%9D%98%20%EC%9B%90%EB%A6%AC#%ED%98%BC%EC%9E%A1-%EC%A0%9C%EC%96%B4-%EB%B0%A9%EC%8B%9D)

네트워크가 혼잡 상태에 이르면 프로세스의 속도를 낮추는 방법 (또한, 3장에서 자세히 다룬다.)