- super()
    
    React.Component상속 클래스는 super(props)를 호출해야 this.props가 정의된다.
    
    construct(여기 들어가는 인자는): 클래스 호출되면서 받아오는 값
    
    super(여기 들어가는 인자는): 부모 클래스에서 가져올 값
    
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
    
    [https://goodmemory.tistory.com/121](https://goodmemory.tistory.com/121)
    
    [https://velog.io/@rand_guy/TILClass에서-Constructor와-Super를-쓰는-이유](https://velog.io/@rand_guy/TILClass%EC%97%90%EC%84%9C-Constructor%EC%99%80-Super%EB%A5%BC-%EC%93%B0%EB%8A%94-%EC%9D%B4%EC%9C%A0)
    
    ---
