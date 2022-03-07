# React-Component

## CONTENTS
1. [super](#super)
2. [prop-types](#prop-types)
3. [react에서 link를 \<a\> 보다 선호하는 이유](#3)
4. [lazy()](#lazy)

### super()
    
  - React.Component상속 클래스는 super(props)를 호출해야 this.props가 정의된다.
    
  - construct(여기 들어가는 인자는): 클래스 호출되면서 받아오는 값
    
  - super(여기 들어가는 인자는): 부모 클래스에서 가져올 값
    
    ```jsx
    class Parent {
        constructor(a,b){
            this.a = a;
            this.b = b;
        }
    
    		sum() {
            return this.a + this.b;
        }
    }
    
    class Child extends Parent {
        constructor(a,b,c){  //이 클래스가 불리려면 3개의 변수가 들어와야함
            super(a,b);     //super키워드를 통해 부모 클래스 생성자 호출
            this.c = c;     //추가 프로퍼티 초기화
        }
    
        avg(){
        	//super.sum()을 통해 부모 클래스의 메소드 접근
            const sum = super.sum() + this.c;
            console.log('평균: '+ sum / 3);
        }
    }
    
    const stu = new Student(0,50,100);
    stu.avg(); //50
    ```
    
 ---
    
  참고
    
  (1) [https://goodmemory.tistory.com/121](https://goodmemory.tistory.com/121)
    
  (2) [https://velog.io/@rand_guy/TILClass에서-Constructor와-Super를-쓰는-이유](https://velog.io/@rand_guy/TILClass%EC%97%90%EC%84%9C-Constructor%EC%99%80-Super%EB%A5%BC-%EC%93%B0%EB%8A%94-%EC%9D%B4%EC%9C%A0)
    
 ---
    
### prop-types
    
- 부모로부터 전달받은 prop의 데이터 type을 검사
- 자식 컴포넌트에서 명시해 놓은 데이터 타입과 부모로부터 넘겨받은 데이터 타입이 일치하지 않으면 콘솔에 에러 경고문이 띄워진다
- proptype에 정의되어있는 타입으로 검사할 수도 있고, 사용자가 함수를 정의할 수도 있다. proptype에 정의되어 있어 이용만 하면 되는 타입은 아래와 같다
        
        ```jsx
        MyComponent.propTypes = {
          // 리액트 요소
          // <div>123</div> , <Component />
          menu: PropTypes.element,
        
          // 컴포넌트 함수가 반환할 수 있는 모든 것(비추)
          // <SomeComponent />, 123
          description: PropTypes.node,
        
          // Message 클래스로 생성된 모든 객체
          // new Messages() -> 참, new Car() -> 거짓
          message: PropTypes.instanceOf(Message),
        
          // 배열에 포함된 값 중에서 하나를 만족
          name: PropTypes.oneOf(["jake", "olivia"]),
        
          // 배열에 포함된 타입 중에서 하나를 만족
          width: PropTypes.oneOfType([PropTypes.number, PropTypes.string])
        
          // 특정 타입만 포함하는 배열
          // [1, 5, 7] -> 참, ['a', 'b'] -> 거짓
          ages: PropTypes.arrayOf(PropTypes.number),
        
          // 객체의 속성값 타입을 정의
          // {color: 'red', weight: 123} -> 참
          info: PropTypes.shape({
            color: PropTypes.string,
            weight: PropTypes.number
          })
        
          // 객체에서 모든 속성값의 타입이 같은 경우
          // {prop1: 123, prop2: 456}
          infos: PropTypes.objectOf(PropTypes.number)
        }
        ```
    ---
    
    참고   
    [https://velog.io/@eunjin/React-PropTypes-쓰는-이유-방법](https://velog.io/@eunjin/React-PropTypes-%EC%93%B0%EB%8A%94-%EC%9D%B4%EC%9C%A0-%EB%B0%A9%EB%B2%95)

    ---
###### 3    
### react에서 link를 \<a\> 보다 선호하는 이유  
    
- a태그: js나 css등 자산을 모두 로드→상태 초기화,재 렌더링 필요→속도 저하
    
- link 컴포넌트: 브라우저의 주소만 변경, 페이지를 불러오는 것이 아닌 업데이트하는 방식→상태유지&속도 증가
    
    ---
    참고
    
    [https://gomgomkim.tistory.com/9](https://gomgomkim.tistory.com/9)
---
### lazy()
- 번들
    
병합된.
    
- lazy
    
    - before: import OtherComponent from './OtherComponent';   

    - after: const OtherComponent = React.lazy(() => import('./OtherComponent'));
    
예시)
    
    import React, { Suspense } from 'react';
    
    const OtherComponent = React.lazy(() => import('./OtherComponent'));
    
    function MyComponent() {
      return (
        <div>
          <Suspense fallback={<div>Loading...</div>}>
            <OtherComponent />
          </Suspense>
        </div>
      );
    }
    
- loding...
    
`Suspense`는 lazy 컴포넌트가 로드되길 기다리는 동안 로딩 화면과 같은 예비 컨텐츠를 보여줄 수 있게 해줍니다.
    
`fallback` prop은 컴포넌트가 로드될 때까지 기다리는 동안 렌더링하려는 React 엘리먼트를 받아들입니다.
    
---
    
참고
    
[https://ko.reactjs.org/docs/code-splitting.html](https://ko.reactjs.org/docs/code-splitting.html)
    
---
