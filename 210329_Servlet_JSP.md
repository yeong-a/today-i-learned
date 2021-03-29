## ✅ Servlet/JSP
- 동적 웹페이지 기술 : JavaEE(Servlet/JSP)
  - 요청이 들어오면 실행해서(프로그램) 결과가 동적으로 생성되는 페이지 <- -> 정적 페이지(html)

### Servelet
- .java <- html 삽입 (출력 스트림에 출력 문자열의 형태)
- html 코드가 길 경우 사용하기 불편함
- XXXServlet.java -> XXXServlet.class

### JSP
- .jsp(html 파일처럼 생각) <- java 삽입
- XXX.jsp -> XXX.java -> XXX.class

## ✅ Servlet Life Cycle
- 직접 필요에 의해 객체생성하는 것이 일반적
- Servlet Container에 의해 객체가 생성되고 메소드가 콜백됨
- [Servlet Interface] -implements-> [GenericSevlet Class] -extends-> [HttpServlet Class] -extends-> [MyServlet Class]: 사용자 정의 Servlet

### doGet(), doPost()
```
doGet(HttpServletRequest req, HttpServletResponse res) {  // req: 요청 메세지, rep: 응답 메세지
    ...
}
```
req, res: 매 요청마다 새로운 객체로 생성되어 전달

## ✅ form data처리
```
reqeust.setCharacterEncoding("utf-8") // post 방식만 유효
// get방식의 인코딩 처리는 서버마다 다름. (표준화 되어있지 않음)

String value = request.getParameter("파라미터 이름");
String[] values = request.getParameterValues("파라미터 이름");
```

## ✅ 응답하기
response 객체 사용: 응답메세지로 생각할 것

1. 응답 컨텐츠 타입을 지시 
  ```
  response.setContentType("text/html;charset="utf-8");  
  response.setContentType("text/xml;charset="utf-8");
  ```
2. 응답 내용을 출력: 출력 스트림을 이용하여 출력
  ```
  Writer out = response.getWriter();  // char 단위 출력(응답)
  OutputStream out = response.getOutputStream();  //byte 단위 출력(응답)
  ```

## ✅ JSP
- Java로 변환될 규칙에 따라 작성하는 템플릿 파일
- JSP 구성요소
  - 선언태그    
  ``` <%! 멤버변수, 메소드 선언 %> ```
  - 지시태그   
  ``` <%@ 지시어 속성이름 = "값" ..... @> ```
  - 스크립트릿   
  ``` <% 자바 실행문장(메소드 안에 작성하는 코드 %> ```
  - 표현태그   
  ``` <%= 출력내용 %> ```
  - 주석   
  ``` <% -- 주석 %> ```
