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

    초기 값을 작성

```
const initialState = { numOfCakes: 10 }
```

    그 다음 함수 작성, reducer는 함수다.

```
   const reducer = (state = initialState, action) => {
       switch(action.type) {
       case BUY_CAKE: return {
           ...state,
           numOfCakes: state.numOfCakes - 1
       }

           default: return state
       }
}
```

3. store를 만들어준다

a. store 만들어준다

```
const createStore = redux.createStore
.
.
.
const store = createStore(reducer)
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
