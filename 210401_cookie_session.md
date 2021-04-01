## ✅ HTTP
- connectless: 연결유지X, req보내고 res받으면 연결해제
- stateless: 상태정보 유지X (기존 req에서 무엇을 했는지 알 수 없음)
-> 단점인듯 하지만, 보완한다면 유한한 네트워크 자원을 효율적으로 사용할 수 있게 해줌

## ✅ Session Tracking
일정 시간동안 동일한 사용자로부터 들어오는 여러 요청들을 하나의 상태로 처리할 수 있도록 지원하는 기술

### 1. Cookie
- client측에 저장
- name, value: 문자열로 저장
- 쿠키는 도메인 별로 유지/관리
- 같은 도메인에서 여러 req를 보낼 때, 같은 도메인에서 생성된 쿠키와 함께 보내짐(만료 시간이 지나지 않은 유효한 쿠키만)
- 서버는 쿠키를 보면 자신의 예전 상태와 작업을 알 수 있음
- 쿠키 만료시간
  - 양수: 유효시간
  - 음수: 세션 쿠키
  - 0: 삭제 
- 보안이 취약해 사용자가 임의로 삭제, 차단 할 수 있으므로 중요한 정보를 저장하면 안됨
- 문자열로만 저장할 수 있어 객체를 저장하는 것이 불편함

``` java
Cookie cookie = new Cookie(name, value);
cookie.setMaxAge(쿠키만료시간);  // 생략하면 Default 음수
res.addCookie();  // 남기고 싶은 쿠키가 여러개면 add를 여러개 해준다.
Cookie[] cookies = req.getCookies();  // 쿠키가 여러개 일 수 있으므로 배열로 선언
```

#### Session Cookie
- 브라우저의 실행 메모리에 저장
- 만료시간을 생략하거나 음수로 주면 생성됨
- 브라우저가 실행되어 있는 동안만 유지

#### 일반 Cookie
- 시스템에 파일로 저장
- 만료시간을 명시하는 경우 생성됨

### 2. Session
- server측에 저장
- 객체 저장 가능
- 여러 상태를 저장할 수 있는 저장 보관함 느낌
- 보통 30분동안 유지됨 (D.D(Web.xml)에서 사용자 정의 할 수 있음)
- 서버 측 부담이 커짐
- 쿠키를 차단하면 세션도 사용이 불가능함 (세션 식별이 불가능하기 때문)

``` java
setAttribute(key, value); // 여러 상태를 저장하고 싶으면 여러번 실행
HttpSesion session = request.getSession(boolean); // 브라우저가 들고 온 세션쿠키를 보고 세션을 찾음. Default 값은 true: 없을 때 세션 생성 여부
session.getAttribute("값");
session.removeAttribute();
session.invalidate(); // 세션 소멸

```
