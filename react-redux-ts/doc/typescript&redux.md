1. rxreducer 를 작성하여, reducer를 생성한다

```
const initialState = {

}

export default (state = initialState, { type, payload }) => {
  switch (type) {

  case typeName:
    return { ...state, ...payload }

  default:
    return state
  }
}
```

2. initialState 의 Interface 작성해준다.

```
interface InitialState {

}
```

\*일부 패키지는 @types 같이 설치해줘야한다

참조
(한글) <br>
React Redux Thunk Typescript 한번에 박살내기
https://youtu.be/qSRPwBrDeXU <br>
리액트 리덕스(Redux)실습강좌 ( 프로젝트에 넣기...) <br>
https://youtu.be/T-q4cmSEX-E <br>
(영어) <br>
https://youtu.be/dZZxegovK9Q
