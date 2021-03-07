---
layout: post
date: 2021-03-05 23:40:00
title: "react-router 외"
author: 김동훈
categories: [TIL]
tags: [github]
image: https://joshua1988.github.io/images/posts/web/javascript/js.png
rating: 4
---

## React-router

이 페이지는 [이 블로그의](https://velopert.com/3417) 내용을 바탕으로 공부한 내용을 기록한 페이지입니다.

### SPA?

Single Page Application의 약자. 1페이지의 페이지로 구성되어 있는 어플리케이션이다.

전통적인 웹어플리케이션의 구조는 여러 페이지로 구성이 되어 있고, 요청할 때마다 페이지가 새로고침(플리커)되고 로딩 할 때마다 서버로부터 리소스를 전달받은 후 렌더하는 과정을 거치게 된다.전통적인 방식은 속도적인 측면에서 문제가 있었고, 서버 자원쪽의 낭비로 이어지기 때문에 요즘에는 잘 사용하지 않는 방식이다.

현대적인 방식은 리액트 같은 프레임워크(혹은 라이브러리)를 사용 해서 뷰 렌더링을 유저의 브라우저가 담당하게 한 후, 정말 필요한 데이터만 전달받아서 보여주게 된다.

싱글페이지라고 해서 한 종류의 화면만 이용할 수는 없기 때문에, 다른 종류의 화면을 이용할 수 있게 '주소'를 만들어야 한다. 주소에 따라서 다른 뷰를 보여 주는 것을 라우팅이라고 하고, 리액트에는 이 기능이 내장되어 있지 않다.
따라서 react-router라는 써드파티 라이브러리를 사용해서 클라이언트 사이드에서 이뤄지는 라우팅을 해야 한다.

`SPA의 단점`

앱의 규모가 커진다면 자바스크립트 파일 사이즈가 커진다는 것.

### Install

```jsx
npm i react-router-dom
```

### How to use?

```jsx
//index.js
import React from "react";
import ReactDOM from "react-dom";
import { BrowserRouter } from "react-router-dom"; // import 한 후
import App from "./App";

ReactDOM.render(
  <React.StrictMode>
    <BrowserRouter>
      {" "}
      //App 컴포넌트를 감싸준다
      <App />
    </BrowserRouter>
  </React.StrictMode>,

  document.getElementById("root")
);
```

`BrowserRouter`

- HTML5의 History API를 이용하여 페이지를 새로고침 하지 않고도 주소변경을 도와준다.
- 현재 주소에 관련된 정보를 props로 조회 및 사용이 가능하게 도와준다.

```jsx
//App.js
import React from "react";
import About from "./About";
import Home from "./Home";
import { Route } from "react-router-dom";

function App() {
  return (
    <div>
      <Route path="/" component={Home} exact />
      <Route path="/about" component={About} />
    </div>
  );
}

export default App;
```

`Route`

- 주소에 따라 다른 화면을 보여주는 라우팅 기능을 가진 컴포넌트
- path=''에는 바뀔 주소의 이름
- component = {}에는 렌더링 될 컴포넌트
- exact = '/about'도 '/'를 포함하고 있기 때문에, 정확히 '/'인것만 렌더하게 도와준다.(exact={true}가 생략되어있다.)

`Link`

- a태그를 사용하여 주소를 바꾸게 될 경우, 상태가 날아가버리고 기존의 렌더된 컴포넌트를 처음부터 다시 진행하게 된다.
- history api만을 사용하여 페이지의 주소만 변경해준다.
- 페이지 전환을 방지해준다.

```jsx
import React from "react";
import About from "./About";
import Home from "./Home";
import { Link, Route } from "react-router-dom";

function App() {
  return (
    <div>
      <div>
        <Link to="/">??</Link>
      </div>
      <div>
        <Link to="/about">??</Link>
      </div>
      <Route path="/" component={Home} exact />
      <Route path="/about" component={About} />
      <Route path={["/about", "hi"]} component={About} /> //1route Npaths
    </div>
  );
}

export default App;
```

## cross-env

흔히 코드를 import 하기 위해 '../directory/directory/file' 이런 식으로 불러 와야 하는 코드에서 '../'부분을 지우기 위한 라이브러리이다.

다시 말해, 프로젝트에서 NODE_PATH를 사용하여 절대경로를 사용 할 수 있게 해주는 라이브러리이다.

```jsx
npm i cross-env --dev
```

package.json의 scripts 부분을 아래와 같이 수정

```jsx
"scripts": {
    "start": "cross-env NODE_PATH=src react-scripts start",
    "build": "cross-env NODE_PATH=src react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  }
```
