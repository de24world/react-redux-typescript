## 1. Reducer 작성

(1) rxreducer 를 작성하여, reducer를 생성한다

PokemonReducers.ts

```
import { POKEMON_FAIL, POKEMON_SUCCESS, PokemonType, PokemonDispatchType } from "../actions/PokemonActionTypes";

const initialState = {
  success: false
}

const PokemonReducer (state = initialState, action: PokemonDispatchType) => {
  switch (action.type) {
    case POKEMON_FAIL:
      return {
        ...state,
        success: false
      }
    case POKEMON_SUCCESS:
      const {abilities, sprites} = action.payload
      return {
        ...state
        success: true,
        pokeomon: {
          abilities,
          sprites
        }
      }
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
  success: boolean
  pokemon: PokemonType
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

export type RootReducerType => ReturnType<typeof rootReducer>

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

## 3. Action 작성

(1) Actions 만들기
PokemonAcions.ts

```
import { Dispatch } from 'redux'
import axios from 'axios'
import { PokemonDispatchType, POKEMON_SUCCESS, POKEMON_FAIL } from './PokemonActionTypes'  ---> (2) Type 만들기 참조

export const fetchPokemonData = ( pokemnoName : string) => async (dispatch: Dispatch<PokemonDispatchType>) => {
  try {
    const res = await.get('....API URL')
    const data = res.data

    dispatch({
      type: POKEMON_SUCCESS,
      payload: data
    })
  } catch (err) {
    dispatch({
      type: POKEMON_FAIL
    })
  }
}

```

(2) Type 만들기
PokemnoActionTypes.ts

```
export const POKEMON_SUCCESS = 'POKEMON_SUCCESS'
export const POKEMON_FAIL = 'POKEMON_FAIL'

<!-- 받아오는 데이터 값의 타입을 정의해준다 -->
export type PokemonAbility = {
  ability: {
    name: string   ("limber)
    url: stinrg    ("https://pokeapi.co/api/v2/ability/7/")
  },
  is_hidden: boolean    (false)
  slot: number  (1)
}

export type PokemonSprites = {
  front_default: string
}

export interface pokemonFailDispatch {
  type: typeof POKEMON_FAIL
}

export interface pokemonSuccessDispatch {
  type: typeof POKEMON_SUCCESS
  payload: {
    abilities: PokemonAbility[]
    sprites: PokemonSprites
  }
}

export type PokemonDispatchType = pokemonFailDispatch | pokemonSuccessDispatch
```

## 4. Component 에서 불러오기 및 사용하기

App.tsx

```
import React from 'react';
import { useSelector } from 'react-redux';
import { RootReducerType } from './Store';
import { fetchPokemonData } from './actions/PokemonActions'

function App() {
  const [pokemonName, setPokemonName] = useState("")
  const pokemonReducer = useSelector((state RootReduceType) => state.PokemonReducer)
  const dispatch = useDispatch()

  const handlePokemoName = (event: React.ChangeEvent<HTMLInputElement>) => {
    setPokemonName(event.target.value)
  }
  const searchButtonTapped = () => {
    dispatch(fetchPokemonData(pokemonName))
  }

  retur (
    <div className="App">
      <input value={pokemonName} onChange={handlePokemoName} />
      <button onClick={searchButtonTapped}>포켓몬찾기</button>
      <div>
        {pokemonReducer.success && <div>
          <p>pokemonName</p>
          {pokemonReducer.pokemon?.abilites.map((ability) => {
            return <div>
            <p>{ability.ability.name}</p>
            <p>{ability.slot}<p>
            </div>
          })}
          <img src={pokemonReducer.pokemon?.sprites.front_default} />
        </div>
      </div>
    </div>
  );
}

export default App;
```

<br>
*일부 패키지는 @types 같이 설치해줘야한다
<br>

참조
(한글) <br>
React Redux Thunk Typescript 한번에 박살내기
https://youtu.be/qSRPwBrDeXU <br>
(영어) <br>
https://youtu.be/dZZxegovK9Q<br>
https://youtu.be/sfmL6bGbiN8
