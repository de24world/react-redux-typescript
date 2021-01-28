1. Action을 작성해준다. (type도)

const BUY_CAKE = 'BUY_CAKE'

function buyCake () {
{
type: BUY_CAKE,
info: 'First redux action;
}
}

2.  reducer를 작성해준다.

        초기 값을 작성

    const initialState = { numOfCakes: 10 }

        그 다음 함수 작성, reducer는 함수다.
        const reducer = (state = initialState, action) => {
        switch(action.type) {
        case BUY_CAKE: return {
            ...state,
        numOfCakes: state.numOfCakes - 1
        }

                default: return state
            }

}

3. store를 만들어준다
