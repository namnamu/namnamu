
# 글로벌 상태 관리 방법(redux/recoil)

- 리덕스
    
    1.  미들웨어
    
    액션이 들어오고 리듀서로 가기 전에 동작을 넣을 수 있다.
    
    비동기 작업 처리.
    
    2.  hook & function
    
    useSelector, useDispatch, useStore & connect()
    
    최적화가 자동으로 되어있어 값이 변할때만 렌더링된다.
    
    3.  모든 글로벌 상태를 하나의 객체로 넣는다.
    
- Context API : 단순한 글로벌 상태 관리
    1. 비동기 작업을 자주하게 된다면 리덕스를 사용하자.
    2. 상태가 바뀌면 Provider 내부 컴포넌트가 모두 리렌더링
    3. 기능별로 context를 생성해야 함.
   
<br/>
<aside>
💡 미들웨어

</aside>

### 정의

- 운영체제와 운영체제에서 실행되는 응용프로그램 사이에서 운영체제의 기능 이외의 서비스를 제공하는 소프트웨어.
- 클라이언트와 서버 간의 통신담당 소프트웨어

### 특징

- 데이터 교환에 일관성 보장

### 종류

- DB : 데이터베이스(sql)와 연결하기 위한 미들웨어
    - JDBC vs ODBC
        
        
        |  | JDBC | ODBC |
        | --- | --- | --- |
        | 구현되는 언어 | java | c, c++, java, etc... |
        | 방식 | 객체지향 | 절차지향 |
        | 지원 웹 서버 | linux기반 | windows |
        
        application-JDBC API-DriverManager-JDBC Driver-SQL
        
        → 데이터베이스와 자바어플리케이션 사이에서 드라이버 연결 등으로 통신역할을 도움. 
        
- RPC :
- MOM :
- TP-Monitor :
- ORB :
- WAS : 웹 어플리케이션 서버
    - [https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html](https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html)
        
        읽어봐야함...ㅠㅠ
        

<aside>
💡 리덕스 미들웨어

</aside>

리덕스에 미들웨어 기능을 할 수있는 핵심 기술이 있는 것이지 리덕스를 미들웨어라고 하기엔 무리가 있지 않을까

`액션-미들웨어-리듀서-스토어`

액션이 디스패치되면 리듀서가 받아와서 업데이트하기 전에 비동기 처리를 위한 작업을 만들 수 있다.

이러한 리덕스 미들웨어는 라이브러리를 사용하기도 한다.

→ [*redux-thunk](https://github.com/reduxjs/redux-thunk), [redux-saga](https://github.com/redux-saga/redux-saga), [redux-observable](https://redux-observable.js.org/), [redux-promise-middleware](https://www.npmjs.com/package/redux-promise-middleware)*

- [redux-logger](https://www.npmjs.com/package/redux-logger)는 뭐지?

# Recoil

리액트 상태관리 라이브러리
