<img src="https://blog.codecentric.de/files/2017/12/Bildschirmfoto-2017-12-01-um-08.56.48.png" width="900" height="400">

1. Action을 작성해준다. (type도)

```
const BUY_CAKE = 'BUY_CAKE'

function buyCake () {
    {
        type: BUY_CAKE,
        info: 'First redux action;
    }
}
```

2.  reducer를 작성해준다.

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

3. store 생성

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

4. 미들웨어 <br>
   redux-logger : 로그(기록)을 남겨준다 <br>
   https://github.com/LogRocket/redux-logger
   <br><br>
   redux-thunk, redux-saga : 비동기 작업을 처리해준다
   참고 자료
   https://react.vlpt.us/
