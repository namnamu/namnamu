# JavaScript

### Contents
- [URLSearchParams()](#urlsearchparams)
- [filter()](#filter)
- [Location객체](#location객체)
- [비동기 async와 await](#비동기-async와-await)

### URLSearchParams()

javascript 에서 url 의 쿼리 파라미터들을 읽거나 수정할떄 사용하는 URLSearchParams 사용법입니다.

주소가 `[http://127.0.0.1/search/?sch_keyword=홍길동&type=1](http://127.0.0.1/search/?sch_keyword=홍길동&type=1)` 일때,

```jsx
sch = location.search; //값은 ?sch_keyword=홍길동&type=1
var params = new URLSearchParams(sch);
var sch_keyword = params.get('sch_keyword'); //값은 '홍길동'
params.set('sch_keyword', '임꺽정');// params의 값은 ?sch_keyword=임꺽정&type=1
```

---

참고

[https://www.fun25.co.kr/blog/javascript-url-query-parameter-reading-updating-urlsearchparams/?page=5](https://www.fun25.co.kr/blog/javascript-url-query-parameter-reading-updating-urlsearchparams/?page=5)

---

### filter()
    
배열출력=배열.filter(배열 구성 요소⇒조건에 충족하면)
  
    const words = [0,1,2,3,4,5];
    const result = words.filter(word => word> 3); // [4,5]

    
---

참고

[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/filter](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

---

### Location객체


    window.location.href            //현재 url

    window.location.protocol        //https:

    window.location.host            //localhost:8080

    window.location.hostname        //localhost

    window.location.port            //8080

    window.location.pathname        // 경로 /project

    window.location.search          //get방식으로 통신하는 파라메터들 ?filter=''

---

참고

url(window.location.href)나 페이지 리다이렉션으로 많이 쓰임.   
실제 코드 사용이랑 어디선가 스쳐지나가면서 본 내용들로 기록

---

### 비동기 async와 await

async : 비동기 처리하고 싶은 함수 앞에 키워드로 작성
        fulfil promise로 리턴함.
promise : 값을 표현하기 위해 .then()사용
        ```
        let hello = async () => { return "Hello" };
        hello().then((value) => console.log(value));   //== hello().then(console.log)
        ```
await : async안에서 비동기 코드 호출
        promise가 fulfil될때까지 중단시킴.       --아마 async함수 내 코드
        다른 실행들은 상관없이 진행.               --아마 async함수 외 코드
        promise기반 함수 앞에 놓을 수 있음.       --아마 놓지 않을 수도 있음
```
return greeting = await Promise.resolve("Hello");
```

* 충분히 이해되지 않음. 직접 테스트가 필요함.

---

참고

https://developer.mozilla.org/ko/docs/Learn/JavaScript/Asynchronous/Async_await

---
