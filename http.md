[전체 notion](https://hvvnsk.notion.site/Chapter-11-e2345ff51f884d1ea0abe3b86403e375)
## HTTP

웹 애플리케이션 계층

웹 브라우저라는 클라이언트를 통해 자유롭게 웹 서핑 할 수 있도록 고안된 통신방식

HTML을 전송하기 위한 프로토콜이지만, 다양한 파일 전송 가능

HTTP의 파일전송은 HTTP Request 와 HTTP Response 를 통해 이루어짐

    

- HTTP 트랜잭션

![Untitled 4](https://user-images.githubusercontent.com/107024718/207652102-bca63d66-72a6-43fd-9fa8-fcdd8fe1cd0e.png)

---

- Request header
    1. Request Line: Method + URI + 버전
    2. 메세지 헤더: 웹브라우저 종류, 버전, 대응 데이터 형식 등의 정보 기술
    3. 공백 라인: 공백이 뜨면 헤더 끝
        
        뒤에 엔티티 바디가 이어짐 ( POST메소드로 데이터 보낼 때처럼 요청과 관련된 내용 )
        
        바디의 Content-type 과 Content-length 의 정보가 헤더에 주어진다.
        
    
- Response header
    1. Response Line: 버전 + 상태코드 + 설명문
    2. 메시지 헤더: 웹 서버 애플리케이션이 자세한 정보 전달하기 위해 이용.
    3. 공백 라인: 공백이 뜨면 헤더 끝
        
        뒤에 엔티티 바디가 이어짐 ( 주로 HTML 파일 )
        
        ![Untitled 5](https://user-images.githubusercontent.com/107024718/207652155-586d7231-a27f-478e-9aa5-36ec52504ac1.png)

        
        상태코드 및 설명문
        

- MIME ( Mulitpurpose Internet Mail Extensions )
    
    이메일 동봉파일을 텍스트 문자로 전환해 전달하기 위해 개발했지만, 현재 범용적으로 활용중.
    
    파일을 텍스트로 인코딩할 때,  [파일의 종류/파일 포맷] 의 content-type을 담는다.
    
    브라우저에서 지원하는 content-type은 열어볼 수 있다.
    
    ![Untitled 6](https://user-images.githubusercontent.com/107024718/207652195-784d11fb-b9cc-4165-9ea6-6b1df1c02987.png)


컨텐츠는 MIME 타입을 갖는 바이트 배열

- CGI ( Common Gateway Interface )
    - 서버가 동적 컨텐츠를 클라이언트로부터 제공받아 다른 컨텐츠 생성하는데 관련 표준.
        ![Untitled 7](https://user-images.githubusercontent.com/107024718/207652227-bbb0b173-e6b2-470b-9354-dcbbb21ff9c1.png)
        ![Untitled 8](https://user-images.githubusercontent.com/107024718/207652279-13f9aead-0b88-4d4c-a1de-9038edd01546.png)

    - CGI 표준을 지키는 프로그램을 CGI 프로그램이라 부른다.
    - 동적으로 프로세스를 생성하여, uri 에 들어온 경로의 프로그램을 실행시킨다.
    - 프로세스의 CGI 환경변수 QUERY_STRING 에 “15000&213” 과 같은 값을 넣고, CGI를 준수하는 프로그램은 이를 받아 위의 CGI 환경변수 그 값을 찾는다.
    - CGI 프로그램은 그 부모가 바디 컨텐츠 종류와 크기를 알게하기 위해 Content-type 과 Content-length 응답 헤더와 헤더 종료 빈 줄까지 생성해야 한다.
