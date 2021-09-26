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

-   dispatch (디스패치)

-   subscribe (구독)
