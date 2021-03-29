## Web Architecture
- Client는 Web Browser에서 발생한 data(Parameter)를 가지고 Server에 요청(request)함
- Web Server(Http Server)에서 Client 접속 처리함 (http, css, js 처리 (DB등을 처리할 수 없음))
- Application Server에서 Presentation(화면에 보여지는 것), Business Logic(일처리), Persistence Logic(DB) 등을 처리 후 Client에게 응답(response)함
- Persistence logic은 JDBC를 이용해 RDBMS와 통신함
- Web Server + Application Server = WAS(Web Application Server)
- Servlet: Web에서 사용할 수 있는 Java api
- JSP(Java Server Page): Servlet을 좀 더 편하게 사용할 수 있게 해주는 api 

### Servlet Interface
Servlet api를 implements하면 다섯개의 메소드를 Override 해야 한다. 메소드는 WAS가 호출한다.
- destroy: Sevlet이 WAS에서 제거될 때 최종적으로 호출되는 메소드 ex) 어떤 객체와의 연결을 끊어라 등
- getSetvelterConfig
- getServletInfo
- init: destroy와 반대 작업을 함. 초기화 작업 수행
- service: client의 요청처리를 함

### GenericServlet Class
- Servlet의 service 메소드를 제외한 메소드를 구현해놓은 클래스
- extends GenericServlet
- HttpServletRequest로 형변환을 해야함
- GET방식 일 때와 POST방식을 나누어서 구현해야 함.

### HTtpServlet Class
- Servlet Interface와 GenericServlet Class보다 사용이 간편함
- abstract Method가 없는 abstract class이기 때문에 원하는 Method를 골라서 구현하면 됨
