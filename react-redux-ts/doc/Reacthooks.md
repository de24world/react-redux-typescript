## 1. useState

state

## 2. useEffect

side Effect

## 3. useContext

## 4. useReducer

simple state & action

```
import React, {useReducer} from 'react'

const initialState = 0
const reducer = (state, action) => {
  switch(action) {
    case 'increment':
      return state + 1
    case 'decrement':
      return state - 1
    case 'reset':
      return initialState
    default state
  }
}

function CounterOne() {
  const [count, dispatch] = useReducer(reducer, initialState)

  return (
    <div>
      <div> Count - {count} </div>
      <button onClick= {()=>dispatch('increment')}> Increment </button>
      <button onClick= {()=>dispatch('decrement')}> Decrement </button>
      <button onClick= {()=>dispatch('reset')}> Reset </button>
    </div>
  )
}

export default CounterOne

```

---

참조
(영어) <br>
Codevolution
https://react-etc.vlpt.us/06.typescript-basic.html <br>
https://react.vlpt.us/using-typescript/01-practice.html <br>
