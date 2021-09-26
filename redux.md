<h1>redux</h1>
1. redux 에서 사용되는 키워드 숙지하기

-   action (액션) : state에 어떠한 변화가 필요하게 될 때 action 을 발생시키게 되고, 하나의 object 로 표현 된다.  
    `{type : "ADD_TODO"}`

    -   action object 는 `type 필드를 필수 적으로 가지고 있어야 하고 그 외의 값은 마음대로 넣어줄 수 있다.

    ```
    {type : "ADD_TODO",
        data: {
            id: 0,
            text: "Redux"
        }
    }
    ```

    -   action creator
        -   action creator function 은, action 을 만드는 function 이다. 단순히 파라미터를 받아와서 action object 형태로 만들어 준다.

    ```
    export function addTodo(data) {
        return {
            type: "ADD_TODO",
            data
        };
    }

    // 화살표 함수로도 만들 수 있다.
    export const editTodo = text => ({
        type: "EDIT_TODO",
        text
    });
    ```

    -   action function 을 만들어서 사용하는 이유는 나중에 component 에서 더욱 쉽게 action 을 발생시키기 위해서이다. 그래서 function 앞에 `export` 키워드를 붙여서 다른 파일에서 불러와서 사용한다. 다만, 필수는 아니다. 직접 object 를 작성 할 수 도 있다.

-   reducer (리듀서)

-   store (스토어)

-   dispatch (디스패치)

-   subscribe (구독)
