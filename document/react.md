# React

### Contents
- [useRef](#useref)
- [useMemo](#usememo)
- [useCallback](#usecallback)
- [useContext](#usecontext)
- [useFetch](#usefetch)


### useRef
    
    1. 특정 DOM 선택하기
    
    버튼 클릭 시, 버튼에 포커스 되던것을 ref를 사용해, 버튼의 입력칸에 포커스되도록
    
    ```
    const nameInput = useRef(); //ref로 선언된 dom을 받아오겠다는 선언
    const onReset = () => {
        nameInput.current.focus(); //이 코드로 들어오기 가장 마지막으로 ref되어있는 dom을 받아옴
      };
    // ...return
    <input
            onChange={onChange}  //값이 입력하는 대로 변하는 기능의 함수
            ref={nameInput}   //참조됨.
          />
    <button onClick={onReset}>초기화</button> //ref를 가진 focus함수 쪽으로 호출
    ```
    
    ---
    
    참고
    
    [https://react.vlpt.us/basic/10-useRef.html](https://react.vlpt.us/basic/10-useRef.html)
    
    ---
    
    ### 2. 컴포넌트 내의 변수 만들기
    
    `useRef` 로 관리하는 변수는 값이 바뀐다고 해서 컴포넌트가 리렌더링되지 않습니다
    
    본디 컴포넌트상태를 바꾸고 렌더링이 되어야 상태가 업데이트 되는 반면,
    
    `useRef` 로 관리하고 있는 변수는 설정 후 바로 조회 할 수 있습니다.
    
    ```
    const nextId = useRef(4);
    ```
    
    →.current의 기본값
    
    이 값을 수정 할때에는 `.current`값을 수정하면 되고 조회 할 때에는 `.current`를 조회하면 됩니다.
    
    ---
    
    참고
    
    [https://react.vlpt.us/basic/12-variable-with-useRef.html](https://react.vlpt.us/basic/12-variable-with-useRef.html)
    
   
### useMemo
    
    ```
    function countActiveUsers(users) {
      console.log('활성 사용자 수를 세는중...');
      return users.filter(user => user.active).length;
    }
    //...component
    const count = countActiveUsers(users); //hook사용전
    //...return
    <input onChange={onChange}/>     //값이 입력될때마다 리렌더링
    <div>활성사용자 수 : {count}</div>
    ```
    
    활성사용자 수가 갱신될때마다 리렌더링 되어야 하는데 input턴에 입력할 때부터 렌더링이 다시 되니까 countActiveUsers가 재 렌더링 됨.
    
    →불필요한 재호출
    
    ```
    const count = useMemo(() => countActiveUsers(users), [users]); //hook사용후
    ```
    
    useMemo(()⇒ 어떻게 연산할지 정의하는 함수, [바뀜을 감지])
    
    배열의 내용이 바뀌지 않았다면 이전에 연산한 값을 재사용하게 된다.
    
    ---
    
    참고
    
    [https://react.vlpt.us/basic/17-useMemo.html](https://react.vlpt.us/basic/17-useMemo.html)
    
### useCallback
    - 렌더링될때마다 필요한 함수들을 재사용하기 쉽도록 함.
    - prps가 바뀌지 않았다면 dom에 새로 렌더링조차 하지 않고 재사용할 수 있도록 최적화하기 위함.
    - useMemo()의 발전된 사용법-좀 더 사용이 쉬움
        - useMemo 는 특정 결과값을 재사용 할 때 사용하는 반면,
        - useCallback 은 특정 함수를 새로 만들지 않고 재사용하고 싶을때 사용합니다.
    
    ```
    // user.id 가 파라미터로 일치하지 않는 원소만 추출해서 새로운 배열을 만듬
    // = user.id 가 id 인 것을 제거함
    
    # 기존 사용법
    const onRemove = id => {
      setUsers(users.filter(user => user.id !== id));
    };
    
    # Hook 사용법
    const onRemove = useCallback(
        id => {
          setUsers(users.filter(user => user.id !== id));
        },
        [users]
      );
    ```
    
    ---
    
    참고
    
    [https://react.vlpt.us/basic/18-useCallback.html](https://react.vlpt.us/basic/18-useCallback.html)
    
### useContext
    
     Provider에 제공한 value가 달라지면 useContext를 쓰고 있는 모든 컴포넌트가 리렌더링 된다
    
    → useMemo와 잘 섞어서 사용할 것.
    
    ```jsx
    // context 값 초기화
    export const PostsContext = createContext(null);
    /*
    -- export로 내보내서 나중에 import { UserDispatch } from './App';로 불러서 사용
    -- React.으로 받아와서 import필요없음
    */
    
    // Context 값 정하기 - Provider
    const Posts = () => {
      const posts = [
        {
          title: 'useContext 알아보기',
          content: '이번 편에서는 React Context를 ...'
        }
      ]
    
      return (
        <PostsContext.Provider value={posts}>
          <Children />
        </PostsContext.Provider>
      )
    }
    /*
    -- 컴포넌트 값을 provider을 이용해 context에 붙여서 postContext에 넘겨준다.
    -- 조회할 컴포넌트를 부르기 이전에 감싸준다.
    */
    
    // context 값 조회1 - Consumer
    <PostsContext.Consumer>
            {posts => {
              let label = 'user'
              if (user.isAdmin) {
                label = 'admin'
              }
    
              return (
                <div>
                  <div>{label}</div>
                  <div>{user.nickname}</div>
                  <div>{posts.map((post, index) => (
                    <div key={index}>
                      <div>{post.title}</div>
                      <div>{post.content}</div>
                    </div>
                  ))}</div>
                </div>
              )
            }}
          </PostsContext.Consumer>
    /*
    -- consumer내에서 provider로 넘겨진 값을 사용할 수 있다.
    */
    
    // context 값 조회2 - useContext
    const Children = () => {
      const user = useContext(AppContext)
      const posts = useContext(PostsContext)
    
      let label = 'user'
      if (user.isAdmin) {
        label = 'admin'
      }
    
      return (
        <div>
          <div>{label}</div>
          <div>{user.nickname}</div>
          <div>{posts.map((post, index) => (
            <div key={index}>
              <div>{post.title}</div>
              <div>{post.content}</div>
            </div>
          ))}</div>
        </div>
      )
    }
    /*
    -- useContext로 context를 받아오면, 바로 조회에 사용할 수 있다.
    */
    ```
    
    Provider 에 의하여 감싸진 컴포넌트 중 어디서든지 우리가 Context 의 값을 다른 곳에서 바로 조회해서 사용 할 수 있습니다.
    
    —그래서 최상단에 provider를 놓고 전역변수처럼 사용하는 느낌인듯.
    
    ---
    
    참고
    
    *** [https://velog.io/@public_danuel/trendy-react-usecontext](https://velog.io/@public_danuel/trendy-react-usecontext)  ***
    
    [https://react.vlpt.us/basic/22-context-dispatch.html](https://react.vlpt.us/basic/22-context-dispatch.html)
    
### useFetch
    1. (X)
    
    이건 사용자 정의 훅같음...
    
    ```jsx
    // 정의
    function useFetch(url) {
      const [payload, setPayload] = useState(null);
      const [loading, setLoading] = useState(true);
      const [error, setError] = useState("");
    
      const callUrl = async () => {
        try {
          const { data } = await Axios.get(url);
          setPayload(data);
        } catch (e) {
          setError("error!!");
        } finally {
          setLoading(false);
        }
      };
    
      useEffect(() => {
        // only did mount
        callUrl();
      }, []);
    
      return { payload, loading, error };
    }
    
    // 사용
    const { payload, loading, error } = useFetch("https://randomuser.me/api/");
    ```
    
    ---
    
    참고
    
     [https://velog.io/@mlsh1112/React-Custom-Hooks-useInput-useFetch](https://velog.io/@mlsh1112/React-Custom-Hooks-useInput-useFetch) 
    
    ---
    
    1. (O)
    
    스포크에서는 use-http에서 임포트해서 사용함.
    
    → [https://use-http.com/#/](https://use-http.com/#/)
    
    - onNewData의 사용
    
    ```jsx
    const {data:todos}=useFetch({
    	path:`통신할 경로?조건으로 5개 페이지씩 가져올 때`,
    	data:[],
    	onNewData:(currData,newData)=>{
    		// if (page===3) return [...currData,newData[0]]
    		/* 위 주석을 풀면,
    				currData=[1,2,3] newData=[4,5,6] updatedData=[1,2,3,4,5,6,7]이라고 설명함.
    				예상컨데, 각 변수에는 위처럼 들어가지만 실제로 가져오는 데이터는 7까지라는 말같다.
    				그 이유가 newData[0]때문이라고 함.
    				그리고, current와 newData가 합쳐져서 todos배열이 되는듯 
    		 */
    		return [...currData,...newData] //개당 가져옴. 아마 currData=1, newData=2
    	}
    },[] //onMount --> 데이터가 선언될때만 useFetch가 일어남.
    )
    ```
    
