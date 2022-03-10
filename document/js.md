# JavaScript

### Contents
- [URLSearchParams()](#urlsearchparams)
- [filter()](#filter)
- [Location객체](#location객체)
- [비동기 async와 await](#비동기-async와-await)
- [EVENT](#event)
- [웹 스토리지](#웹-스토리지)
- [fetch()](#fetch)


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

| async   

- 비동기 처리하고 싶은 함수 앞에 키워드로 작성.

- fulfil promise로 리턴함.

| promise   
- 값을 표현하기 위해 .then()사용.

```jsx
let hello = async () => { return "Hello" };

hello().then((value) => console.log(value));   //== hello().then(console.log)
```

| await 

- async안에서 비동기 코드 호출.

- promise가 fulfil될때까지 중단시킴.         --아마 async함수 내 코드.

- 다른 실행들은 상관없이 진행.                 --아마 async함수 외 코드.

- promise기반 함수 앞에 놓을 수 있음.         --아마 놓지 않을 수도 있음.

```
return greeting = await Promise.resolve("Hello");
```
<br/>
<aside>
💡 충분히 이해되지 않음. 직접 테스트가 필요함

</aside>

---

참고

https://developer.mozilla.org/ko/docs/Learn/JavaScript/Asynchronous/Async_await

---

### EVENT

- preventDefault()
    
    이벤트를 막는다.
    
    ```jsx
    function checkName(evt) {
      var charCode = evt.charCode;
        if (charCode < 97 || charCode > 122) {
          evt.preventDefault();//이벤트가 막히고 아래 기능만 함.
          displayWarning(
            "영문 소문자만 입력하세요."
            + "\n" + "charCode: " + charCode + "\n"
          );
        }
    }
    ```
    
    ---
    
    참고
    
    [https://developer.mozilla.org/ko/docs/Web/API/Event/preventDefault](https://developer.mozilla.org/ko/docs/Web/API/Event/preventDefault)
   
   ---
    

### 웹 스토리지
- localStorage
    
    웹스토리지: 세션스토리지,로컬스토리지
    
    - 세션 스토리지: 세션끝나면 지워짐
    
    브라우저에서 같은 웹사이트를 여러 탭이나 창에 띄우면, 여러 개의 세션 스토리지에 데이터가 서로 격리되어 저장. 각 탭이나 창이 닫힐 때 저장해 둔 데이터도 함께 소멸합니다. 
    
    - 로컬스토리지: 세션끝나도 안지워짐
    
    반면에, 로컬 스토리지의 경우 여러 탭이나 창 간에 데이터가 서로 공유되며 탭이나 창을 닫아도 데이터는 브라우저에 그대로 남아 있습니다.
    
    따라서 직접 청소해줘야합니다.
    
    주의: 모든 것이 문자형으로 저장된다.
    
    ```
    // 키에 데이터 쓰기
    localStorage.setItem("key", value);
    
    // 키로 부터 데이터 읽기
    localStorage.getItem("key");
    
    // 키의 데이터 삭제
    localStorage.removeItem("key");
    
    // 모든 키의 데이터 삭제
    localStorage.clear();
    
    // 저장된 키/값 쌍의 개수
    localStorage.length;
    ```
    
    ---
    
    참고
    
    [https://www.daleseo.com/js-web-storage/](https://www.daleseo.com/js-web-storage/)
---
### fetch()
1.fetch("http:~")    

 굳이 라이브러리를 사용하면 자바스크립트의 번들파일의 크기만 늘려서 낭비가 될 수 있다.
    
   브라우저의 window객체에 소속되어 window.fetch()으로 사용가능
    
   - 첫번째 인자: url   
   - 두번째 인자: option   
        - HTTP방식, HTTP요청 헤더, HTTP요청 전문(body) 설정   
   - 반환 객체: promise   
        - api호출 성공: 응답객체(response)를 resolve   
            - HTTP응답상태(status), HTTP응답헤더, HTTP응답전문 등 읽기 가능   
        - api호출 실패: 예외객체(error)를 reject   
    
   **GET사용방식**
    
 ```
   fetch("https://jsonplaceholder.typicode.com/posts/1").then((response) =>
     console.log(response)
   );
 ```
    
 **POST사용방식**
    
 ```
 fetch("https://jsonplaceholder.typicode.com/posts", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        title: "Test",
        body: "I am testing!",
        userId: 1,
      }),
    }).then((response) => console.log(response));
```
    
  ---
    
   참고
    
   [https://www.daleseo.com/js-window-fetch/](https://www.daleseo.com/js-window-fetch/)
    
   ---
    
2. fetch(경로)
    
    json파일에 쉽게 접근할 수 있다.
    
    ```jsx
    function loadItems(){
    	return fetch("data/data.json")
    	.then((response)=>response.json())
    	.then((json)=>json.items);
    }
    //아이템 동적으로 받아오기
    loadItems().then((items)=>{
    	console.log(items);
    });
    ```
    
    then으로 받아온 response에는 url과 status가 들어있다. 
    
    .json()을 통해 json형태로 변환할 수 있다.
    
    ---
    
    참고
    
    [https://namhandong.tistory.com/99](https://namhandong.tistory.com/99)
    
    ---
