---
layout: post
date: 2020-12-24 24:00:00
title: "Redux Basic "
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

- action : 리듀서에게 어떤 행동을 해야 할지 전해주는 역할

  ```jsx
  const action = "ACTIOM";
  ```

- dispatch : reducer에 액션을 전해주는 역할

  ```jsx
  store.dispatch({ type: changeState });
  ```

- subscribe : store의 상태가 변할 때, 실행되는 함수 ⇒ useState에서의 state 느낌

  ```jsx
  const initialState = 초기값;
  const [state, setState] = useState(initialState);
  console.log(store.subscribe === state); /// 초기값
  ```

  ### src/components

```jsx
//index.tsx

import React from "react";
import ReactDOM from "react-dom";
import App from "./App";
import { Provider } from "react-redux";
import { createStore } from "redux";
import rootReducer from "./modules";

const store = createStore(rootReducer); //store 생성(rootrudecer)

ReactDOM.render(
  <Provider store={store}>
    {" "}
    //APP을 Provider 로 감싸줘서 스토어 적용
    <App />
  </Provider>,
  document.getElementById("root")
);
```

```jsx
//App.tsx
import React from "react";
import TabContainer from "./containers/TabContainer";

function App() {
  return (
    //액션과 리듀서 코드를 가지고 있는 TabContainer를 임포트 해서 사용
    <div className="App">
      <TabContainer />
    </div>
  );
}

export default App;
```

```jsx
//TabContainer.tsx
import React from "react";
import { useSelector, useDispatch } from "react-redux";
import { RootState } from "../modules";
import { changeTabAction } from "../modules/changeTab";
import Tabs from "../components/Tabs";

const TabContainer = () => {
  const tabState = useSelector((state: RootState) => state.changeTab.tab);
  //useSelector를 통해 현재 State값을 가져옴
  //state === rootReducer라고 생각, rootReducer에서 changeTab을 가져옴
  //changeTab은 tab에 해당하는 상태를 가지고 있음

  const dispatch = useDispatch(); // 디스패치 함수를 가져옵니다

  // 각 액션들을 디스패치하는 함수들을 만들어줍니다

  const setTab = (tab: string) => {
    dispatch(changeTabAction(tab));
  };
  //state의 값을 tab으로 변경

  return <Tabs tabState={tabState} setTab={setTab} />;
};

export default TabContainer;
```

```jsx
//Tabs.tsx
import React from 'react';

interface CounterProps {
  tabState : string
  setTab: (tab: string) => void;
}

function Counter({
  tabState,setTab
}: CounterProps) {
  return (
    <div>
      <h1>탭 : {tabState}</h1>
      <button value='1' onClick={(e : any) => setTab(e.target.value)}>1번탭</button>
      <button value='2' onClick={(e : any) => setTab(e.target.value)}>2번탭</button>
      <button value='3' onClick={(e : any) => setTab(e.target.value)}>3번탭</button>

    </div>
  );
}

export default Counter;
```

### src/modules

```jsx
//changeTab.ts

const TAB_CHANGE = 'counter/TAB_CHANGE' as const;

export const changeTabAction = (tab: string) => ({
    type: TAB_CHANGE,
    payload: tab
  });

  type TabAction =
  | ReturnType<typeof changeTabAction>;
  type TabState = {
    tab: string;
  };

  // 초기상태를 선언합니다.
  const initialState: TabState = {
    tab: '1'
  };

  function changeTab(state: TabState = initialState,action: TabAction): TabState {
    switch (action.type) {

      case TAB_CHANGE:
        return { tab: action.payload};
      default:
        return state;
    }
  }

  export default changeTab;
```

```jsx
//index.ts

import { combineReducers } from "redux";
import changeTab from "./changeTab";

const rootReducer = combineReducers({
  changeTab,
});

export default rootReducer;

export type RootState = ReturnType<typeof rootReducer>;
```

- 스토어는 어떻게 생성하고 어디에 사용하는지
- 액션은 어떻게 생성하고 어떤역할을 하는지
- useSelector, dispatch를 어떻게 사용 하는지

어떻게 따라치면서 하긴 했는데.. 기본개념이 너무 약한것 같다.

하나씩 차근차근 하면서 리덕스를 몸에 익힐 것!
