---
layout: post
date: 2021-04-09 23:40:00
title: "Redux-Repeat"
author: 김동훈
categories: [TIL]
tags: [github]
image: https://redux.js.org/img/redux-logo-landscape.png
rating: 3
---

- store : 상태값을 저장

  ```jsx
  const store = createStore(reducer);
  ```

- Reducer : 상태를 변경 하는 함수 ⇒ useState에서의 setState느낌

  ```jsx
  const reducer = (state = initialState, action) => {
    switch (action.type) {
      case "TYPE":
        return changeState;
      default:
        return state;
    }
  };
  ```

- action :

  리듀서에게 어떤 행동을 해야 할지 전해주는 역할

  type값을 반드시 가지고 있는 하나의 객체로 표현된다.

  ```jsx
  {
    type: "TYPE";
  }
  ```

- action creator :

  액션을 만드는 함수

  ```jsx
  export const actionCreator = (text) => ({
    type: "TYPE",
    text,
  });
  ```

- dispatch :

  store의 내장 함수로 reducer에 액션을 전해주는 역할

  ```jsx
  store.dispatch({ type: "TYPE" });
  ```

- subscribe :

  store의 상태가 변할 때, 실행되는 함수 ⇒ useState에서의 state 느낌

  리액트에서 이 함수를 직접 사용하게 될 일은 별로 없다. react-redux에서 제공하는 connect 함수 또는 useSelector hook을 사용해서 리덕스 스토어 상태를 받아온다.

  ```jsx
  const initialState = 초기값;
  const [state, setState] = useState(initialState);
  console.log(store.subscribe === state); /// 초기값
  ```

  ***

  21.04.09 추가

  면접이 괜찮게 진행되고 있었는데, 리덕스의 플로우를 설명해주세요 에서 막혔다. 기본적인 용어도 생각이 나질 않고 용어가 생각이 나질 않으니 플로우가 그려지는것이 이상할 정도였다. 물론 면접관분들이 이해해주셔서 넘어갔지만, 결국 대답을 제대로 하지 못한 것이기 때문에 이 부분을 추가 해야 하는 필요를 느꼈다. 결국 설명이 되어야 내가 아는것이기 때문에..

  1. 타입을 선언한다.

     ```jsx
     const TYPE = "TYPE";
     ```

     1-1. 타입스크립트일 경우, 액션의 타입을 선언해야 한다.(선언하지 않으면 TYPE을 스트링타입으로 반환한다.)

     ```tsx
     const TYPE = "TYPE" as const

     type typeOfAction = {
     	| ReturnType <typeof 리듀서함수>
     }
     ```

  2. 액션 생성 함수를 만든다.

     ```tsx
     const actionCreator = () => ({ type: TYPE });
     ```

  3. state의 초기값을 설정한다.

     ```tsx
     const initialState = {
       key: 초기값,
     };
     ```

  4. 리듀서 함수를 만든다.

     ```tsx
     const reducerFunction = (state=initialState, action:typeOfAction){
     	switch (action.type){// if action에 타입이 있으면
     		case TYPE:
     			return {key:변경될 키 값}
     		default://기본값
     			return state
     	}
     }
     ```

  5. 루트리듀서에 리듀서를 export 한다.(스토어가 하나의 리듀서를 받기 때문에, 리듀서를 하나로 모아주는 역할)
  6. useSelector를 사용해서 변수를 선언하고

     ```tsx
     const practice = useSelector((state) => state.reducerFunction.key);
     ```

  7. 객체 생성 함수를 useCallback을 이용해 값을 내보낸다.

  `리덕스 카운터 및 투두리스트 제대로 다시 만들어 볼 것!`
