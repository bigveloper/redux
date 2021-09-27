<h1>redux</h1>
1. redux 에서 사용되는 키워드 숙지하기

-   action (액션) : state에 어떠한 변화가 필요하게 될 때 action 을 발생시키게 되고, 하나의 object 로 표현 된다.  
    `{type : "ADD_TODO"}`

    -   action object 는 `type 필드를 필수 적으로 가지고 있어야 하고 그 외의 값은 마음대로 넣어줄 수 있다.

    ```javascript
    {type : "ADD_TODO",
        data: {
            id: 0,
            text: "Redux"
        }
    }
    ```

    -   action creator
        -   action creator function 은, action 을 만드는 function 이다. 단순히 파라미터를 받아와서 action object 형태로 만들어 준다.

    ```javascript
    export function addTodo(data) {
        return {
            type: 'ADD_TODO',
            data,
        };
    }

    // 화살표 함수로도 만들 수 있다.
    export const editTodo = (text) => ({
        type: 'EDIT_TODO',
        text,
    });
    ```

    -   action function 을 만들어서 사용하는 이유는 나중에 component 에서 더욱 쉽게 action 을 발생시키기 위해서이다. 그래서 function 앞에 `export` 키워드를 붙여서 다른 파일에서 불러와서 사용한다. 다만, 필수는 아니다. 직접 object 를 작성 할 수 도 있다.

-   reducer (리듀서) : reducer 는 변화를 일으키는 function 이다. 두가지의 파라미터를 받아온다.

    ```javascript
    function counter(state, action) {
        switch (action.type) {
            case 'INCREASE':
                return state + 1;
            case 'DECREASE':
                return state - 1;
            default:
                return state;
        }
    }
    ```

    -   reducer 는 `현재의 state` 와 `전달 받은 action` 을 참고하여 `새로운 state` 를 만들어서 `반환` 한다. useReducer 를 사용할 때 작성하는 reducer 와 똑같은 형태를 가지고 있다.
    -   useReducer 에서는 일반적으로 `default:` 부분에 `throw new Error('Unhandled Action')` 과 같이 에러를 발생 시키도록 처리하는게 일반적이나, `redux` 의 `reduce` 에서는 기존 state 를 반환 하도록 작성 해야 한다.
    -   redux 를 사용 할 때는 여러개의 reducer 를 만들고 이를 합쳐서 Root Reducer 를 만들 수 있다. (Root Reducer 안의 reducer 들을 sub reducer 라고 부른다.)

-   store (스토어) : `redux` 에서는 각 `Application` 당 `하나의 store` 을 만든다. store 안에는 `현재의 앱 상태`와, `reducer` 가 들어가 있고, 추가적으로 `몇가지 내장 함수`들이 있다.

-   dispatch (디스패치) : `dispatch` 는 `store 의 내장함수 중 하나`이다. `dispatch` 는 `action 을 발생 시키는 것`으로 이해 하면 된다. `dispatch` 함수에는 `action 을 파라미터로 전달`한다. `dispatch(action)` 이런 식이다.

-   subscribe (구독) : subscribe 또한 store 의 내장함수 중 하나이다. subscribe 함수는, 함수 형태의 값을 파라미터로 받아온다. subscribe 함수에 특정 함수를 전달해주면, action 이 dispatch 되었을 때마다 전달해준 함수가 호출된다.
    -   react 에서 redux 를 사용하게 될 때는 이 함수를 직접 `사용하는 일은 별로 없다`고 하지만 `react-redux라는 라이브러리`에서 제공하는 `connect 함수` 또는 `useSelector 라는 Hook` 을 사용하여 `redux store`의 `state` 에 `subscribe` 한다.

2. redux 모듈 만들

-   react project 에 redux 를 적용하기 위해 redux 모듈을 만들어 본다.
-   redux 모듈이란 다음 항목들이 들어있는 자바스크립트 파일을 의미한다.

    -   action type
    -   action creator function
    -   reducer

-   redux 를 사용하기 위해 위 항목들은 각각 다른 파일에 저장할 수도 있다.

-   action 과 reducer를 서로 다른 파일에 정의 할 수 있다. 하지만, 이 코드들이 꼭 분리되어 있을 필요는 없다. 이 코드들이 서로 다른 directory 에, 그리고 서로 다른 파일에 분리가 되어 있으면 개발하는데 꽤나 불편하다. `action` 과 `reducer` 관련 코드들을 `하나의 파일에 몰아서 작성`할 수 있는데 이를 `Ducks pattern` 이라고 부른다. `redux 관련 코드를 분리하는 방식은 정해져 있지 않다.`
