---
layout: post
date: 2020-12-24 24:00:00
title: 'Redux Basic '
author: 김동훈
categories: [TIL]
tags: [github]
image: https://redux.js.org/img/redux-logo-landscape.png
rating: 2
---

# Redux Basic
---

- store : 상태값을 저장

    ```jsx
    const store = createStore(reducer)
    ```

- Reducer : 상태를 변경 하는 함수 ⇒ useState에서의 setState느낌

    ```jsx
    const reducer = (state = initialState, action) => {
    	switch(action.type){
    		case "TYPE" : 
    			return changeState;
    		default : 
    			return state
    	}
    }
    ```

- action : 리듀서에게 어떤 행동을 해야 할지 전해주는 역할

    ```jsx
    const action = "ACTIOM"
    ```

- dispatch : reducer에 액션을 전해주는 역할

    ```jsx
    store.dispatch({type:changeState})
    ```

- subscribe : store의 상태가 변할 때, 실행되는 함수 ⇒ useState에서의 state 느낌

    ```jsx
    const initialState = 초기값
    const [state, setState] = useState(initialState)
    console.log(store.subscribe === state) /// 초기값
    ```
