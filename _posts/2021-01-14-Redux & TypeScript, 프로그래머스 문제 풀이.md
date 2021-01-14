---
layout: post
date: 2021-01-14 23:40:00
title: "Redux & TypeScript, 프로그래머스 문제 풀이 "
author: 김동훈
categories: [TIL]
tags: [github]
image: https://redux.js.org/img/redux-logo-landscape.png
rating: 5
---

## Redux & TypeScript

### 액션 type 선언

- 액션의 type 선언 > typescript의 타입이 아닌 액션 안에 들어가게 될 type 값
- it needs `as const`
- as const를 사용하지 않는 다면 그냥 string type이 되지만 as const를 사용한다면 액션의 타입값을 그대로 가지게 된다.

```jsx
const INCREASE = 'action'
const INCREASE = 'directory/INCREASE' as const
```

### 액션 객체 생성 함수

```jsx
export const increase = (diff:number) => ({
		type : INCREASE
		payload : diff
})
```

- diff라는 값을 변수로 가지는 객체 생성 함수
- payload는 FSA 규칙을 따르기 위함이라고 한다. 이 규칙을 따름으로써 액션 객체의 구조를 일관성 있게 가져갈 수 있다.

### Typescript type 선언

```jsx
type CounterAciton = ReturnType<typeof increase>;

//type 대신 interface 사용 가능
```

### 상태의 type

```jsx
type CounterState = {
  count: number,
};

const initialState: CounterState = {
  count: 0,
};

//type 대신 interface 사용 가능
```

### RootState type

```jsx
export type RootState = ReturnType<typeof rootReducer>;
```

- useSelector를 할 때 필요한 부분

---

- 기본적으로는 자바스크립트의 리덕스랑 큰 차이는 없었다. (RootState정도?)
- ts가 된 만큼 액션타입, 상태타입, 타입스크립트의 타입, rootState 타입을 잘 구분해야 할 필요가 있었다.
- 스토어를 만들고 (자바스크립트 리덕스랑 똑같다)
- 액션을 만들고 (액션 타입을 as const로 만들어 줘서 액션의 타입을 만들 때 섞이지 않게 한다.)
- 액션 객체 생성 함수를 만든다. diff와 같이 변수가 있다면 type 뿐만이 아니라 payload까지 같이 신경을 쓴다.
- 리듀서를 만든다(자바스크립트 리덕스랑 똑같다.
- 루트리듀서를 만들고 (자바스크립트 리덕스랑 똑같다.) RootState를 만든다.
- 컨테이너에서 컴포넌트를 불러 오고, dispatch, useSelector, 객체 생성 함수 등을 만들어 내려준다.

---

## 예산

### **문제 설명**

S사에서는 각 부서에 필요한 물품을 지원해 주기 위해 부서별로 물품을 구매하는데 필요한 금액을 조사했습니다. 그러나, 전체 예산이 정해져 있기 때문에 모든 부서의 물품을 구매해 줄 수는 없습니다. 그래서 최대한 많은 부서의 물품을 구매해 줄 수 있도록 하려고 합니다.

물품을 구매해 줄 때는 각 부서가 신청한 금액만큼을 모두 지원해 줘야 합니다. 예를 들어 1,000원을 신청한 부서에는 정확히 1,000원을 지원해야 하며, 1,000원보다 적은 금액을 지원해 줄 수는 없습니다.

부서별로 신청한 금액이 들어있는 배열 d와 예산 budget이 매개변수로 주어질 때, 최대 몇 개의 부서에 물품을 지원할 수 있는지 return 하도록 solution 함수를 완성해주세요.

### 제한사항

- d는 부서별로 신청한 금액이 들어있는 배열이며, 길이(전체 부서의 개수)는 1 이상 100 이하입니다.
- d의 각 원소는 부서별로 신청한 금액을 나타내며, 부서별 신청 금액은 1 이상 100,000 이하의 자연수입니다.
- budget은 예산을 나타내며, 1 이상 10,000,000 이하의 자연수입니다.

---

### 입출력 예

| d           | budget | result |
| ----------- | ------ | ------ |
| [2,2,3,3]   | 10     | 4      |
| [1,3,2,5,4] | 9      | 3      |

### 입출력 예 설명

입출력 예 #1각 부서에서 [1원, 3원, 2원, 5원, 4원]만큼의 금액을 신청했습니다. 만약에, 1원, 2원, 4원을 신청한 부서의 물품을 구매해주면 예산 9원에서 7원이 소비되어 2원이 남습니다. 항상 정확히 신청한 금액만큼 지원해 줘야 하므로 남은 2원으로 나머지 부서를 지원해 주지 않습니다. 위 방법 외에 3개 부서를 지원해 줄 방법들은 다음과 같습니다.

- 1원, 2원, 3원을 신청한 부서의 물품을 구매해주려면 6원이 필요합니다.
- 1원, 2원, 5원을 신청한 부서의 물품을 구매해주려면 8원이 필요합니다.
- 1원, 3원, 4원을 신청한 부서의 물품을 구매해주려면 8원이 필요합니다.
- 1원, 3원, 5원을 신청한 부서의 물품을 구매해주려면 9원이 필요합니다.

3개 부서보다 더 많은 부서의 물품을 구매해 줄 수는 없으므로 최대 3개 부서의 물품을 구매해 줄 수 있습니다.

입출력 예 #2모든 부서의 물품을 구매해주면 10원이 됩니다. 따라서 최대 4개 부서의 물품을 구매해 줄 수 있습니다.

### 코드

```jsx
function solution(d, budget) {
  var answer = 0;
  var number = 0;
  d.sort((a, b) => a - b);
  for (let i = 0; i < d.length; i += 1) {
    answer = answer + 1;
    number = number + d[i];
    if (number > budget) {
      return answer - 1;
    } else if (number === budget) {
      return answer;
    }
  }
  return answer;
}
```

- 처음에는 배열에서 수를 골라 계속 더하고 결과 확인하는 재귀를 사용하려고 했다. 근데 몇개의 수를 골라야 할지도 모르겠고.. 수를 고른다고 해도 어떻게 재귀를 사용해야 할 지 감이 잡히질 않았다.
- 그래서 검색을 해보니.. 아예 생각부터가 잘못됐었다. ([참고블로그](https://boycoding.tistory.com/240))
- 우선 정렬을 하고, 하나씩 더하다보면 언젠가는 예산을 넘어서게 된다.(예산 신청의 총 합이 예산보다 큰 경우)
- 예산 신청을 더할때마다 ++을 해주니 예산을 넘어서게 될 경우에는 가장 마지막의 카운터 하나를 빼준다.
- 만약에 예산과 예산 신청이 똑같을 경우에는 더한 그대로의 것을 리턴한다.
