## 1. Reducer 작성

(1) rxreducer 를 작성하여, reducer를 생성한다

PokemonReducers.ts

```
const initialState = {

}

const PokemonReducer (state = initialState, action: any) => {
  switch (action.type) {


  default:
    return state
  }
}

export default PokemonReducer
```

(2) initialState 의 Interface 작성해준다. <br>
PokemonReducers.ts

```
interface InitialState {

}
```

(3) Reducer가 여러 개면 combineReducers 로 묶어준다. <br>
reducers/index.ts

```
import PokemonReducer from './PokemonReducer'
import { combineReduers } from 'redux'

const rootReducer = combineReducers({
  PokemonReducer
  ...
})

export default rootReducer
```

## 2. Store 작성

(1) Store 파일 작성 <br>
Store.ts

```
import { applyMiddleware, createStore } from 'redux'
import rootReducer from './reducers/index'
import thunk from 'redux-thunk'

const store = createStore(rootReducer,  applyMiddleware(thunk))

export default store
```

(2) Provider 를 App을 감싸준다 <br>
index.tsx

```
import './index.css';
import App from './App';
import React from 'react';
import ReactDOM from 'readt-dom';
import store from './Store';
import { Provider } from 'react-redux';

<Provider store={store}>
  <App />
</Provider>

```

## 3. Store 작성

<br>
*일부 패키지는 @types 같이 설치해줘야한다
<br>

참조
(한글) <br>
React Redux Thunk Typescript 한번에 박살내기
https://youtu.be/qSRPwBrDeXU <br>
리액트 리덕스(Redux)실습강좌 ( 프로젝트에 넣기...) <br>
https://youtu.be/T-q4cmSEX-E <br>
(영어) <br>
https://youtu.be/dZZxegovK9Q
