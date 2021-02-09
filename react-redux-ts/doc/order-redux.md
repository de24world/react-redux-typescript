<img src="https://blog.codecentric.de/files/2017/12/Bildschirmfoto-2017-12-01-um-08.56.48.png" width="900" height="400">

## 1. Action을 작성해준다. (type도)

```
const BUY_CAKE = 'BUY_CAKE'

function buyCake () {
    {
        type: BUY_CAKE,
        info: 'First redux action;
    }
}
```

- data(payload, info) 값을 동적(계속)으로 변경하고 싶다면 데이터 값을 파라미터로 넘겨준다

```
const changeNickname(data) => {
    return {
        type: "CHANGE_NICKNAME',
        data,
    }
}

changeNickname('boogicho');
// {
//  type: "CHANGE_NICKNAME",
//  data: "boogicho',
// }
```

## 2. reducer를 작성해준다. (이전상태, 액션) => 다음 상태로 바꿔주는 함수

    a. 초기 값을 작성

```
const initialState = { numOfCakes: 10 }
```

    b. 그 다음 함수 작성, reducer는 함수다.

```
   const cackeReducer = (state = initialState, action) => {
       switch(action.type) {
       case BUY_CAKE: return {
           ...state,
           numOfCakes: state.numOfCakes - 1
       }

           default: return state
       }
}
```

c. reducer 가 여러개면 하나로 묶어준다

    ```
    const combineReducers =  redux.combineReducers
    .
    .
    .
    const rootReducer = combineReducers({
      cake: cackeReducer,
      iceCream: iceCreamReducer
    })

## 3. store 생성

a. store 만들어준다

```
const createStore = redux.createStore
.
.
.
const store = createStore(rootReducer)
```

b. subscribe 해준다. <br>
subscribe : from 'Store' to 'View(Component)'

```
store.subscribe(()=>console.log('Update state', store.getState()))
```

c. dispatch 해준다 <br>
dispatch from 'View(Component)' to 'Store'

```
store.dispatch(buyCake())
store.dispatch(buyCake())
```

4. connect 이용하여 리액트 컴포너틑에 넘기기 <br>
   mapStateToProps : Redux state 값을 React props로 전달 = useSelect<br>
   mapDispatchToProps : Redux dispatch 변경 값을 React props로 전달. = useDispatch <br> 예를 들어 component 내 에서 변경된 값을 reducer로 전달하여 다시 변경할 수도 있다. (https://youtu.be/T-q4cmSEX-E 28분경 참조)

```
import { connect } from 'react-redux'
import { addSubscriber } from '../redux/subscribers/actions'
const Subscribers = (props) => {
    return (
        <div>
            <h2> 구독자 수  {props.count} </h2>
            <button> onClick={() => props.addSubscriber()}
        </div>
    )
}

const mapStateToProps = (state) => {
    return {
        count.state.count
    }
}

const mapDispatchToProps = (dispatch) => {
    return {
        addSubscriber: () => dispatch(addSubscriber())
    }
}

export default connect(mapStateToProps)(Subscribers)

```

## 5. 미들웨어 <br>

참조 : https://velopert.com/3401 <br>
미들웨어 대표적인 3가지 <br>
redux-logger : 로그(기록)을 남겨준다 <br>
https://github.com/LogRocket/redux-logger
<br>
redux-thunk, redux-saga : 비동기 작업을 처리해준다 <br>
두가지 차이 : https://velog.io/@dongwon2/Redux-Thunk-vs-Redux-Saga%EB%A5%BC-%EB%B9%84%EA%B5%90%ED%95%B4-%EB%B4%85%EC%8B%9C%EB%8B%A4-
<br>
참고 자료 <br>
https://react.vlpt.us/

<br>
사용하고자 하는 미들웨어를 applyMiddleware 와 함께 Store에 넣어준다. 예 : logger

```
<!-- store.js -->
import { createStore, applyMiddleware } from 'redux'
import rootReducer from './rootReducer'
<!-- rootReducer에는 reducer를 컴바인시켜주었다 -->
import logger from 'redux-logger'

const middleware = [logger]

const store = createStore(rootReducer, applyMiddleware(...middleware))

export default store;
```

리덕스 폴더구조 <br>
Rails Style: 폴더들을 “actions”, “constants”, “reducers”, “containers”, “components” 로 구분합니다. <br>
Domain Style: 폴더들을 기능이나 도메인 단위로 구분합니다. 각각의 폴더에 파일 타입별로 하위 폴더가 있을 수 있습니다. <br>
“Ducks”1: domain-style과 비슷하지만, 명확하게 액션과 리듀서를 함께 묶습니다. 대부분 같은 파일 안에 정의됩니다. <br>
https://livebook.manning.com/book/redux-in-action/chapter-11/20

<br>
참조
(한글) <br>
리액트 리덕스(Redux)실습강좌 ( 프로젝트에 넣기...) <br>
https://youtu.be/T-q4cmSEX-E <br>
