# JavaScript

### URLSearchParams

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
