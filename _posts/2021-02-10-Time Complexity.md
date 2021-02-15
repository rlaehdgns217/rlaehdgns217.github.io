---
layout: post
date: 2021-02-09 23:40:00
title: "Time Complexity"
author: 김동훈
categories: [TIL]
tags: [github]
image: https://images.ctfassets.net/cnu0m8re1exe/4tflobsiQoaB0eBIZr4T7Z/8400a2fa8d6c7db34fcfd7375458a35e/shutterstock_112763713.jpg?w=650&h=433&fit=fill
rating: 3
---

## Time Complexity

- 시간복잡도
  '입력값이 증가하거나 감소함에 따라 시간이 얼마나 비례해서 증가하거나 감소하는가?'
  를 수학적으로 어떻게어떻게 표현한 것이 시간복잡도라고 할 수 있다. 보통은 최악의 경우를 나타내는 Big O 표기법으로 표기를 한다.
  결과를 반환 하는데 최선의 경우 1초 평균의 경우 10초, 최악의 경우 100초인 알고리즘을 백번 실행 한다고 했을 때, 최선의 경우로만 생각한다면 100초 안에 끝나야 하지만 100초를 넘길 확률이 훨씬 크다. 최악의 경우가 발생하지 않는 것을 생각하는 것 보다는 최악의 경우도 고려하여 대비하는 측면이라고 하는 것이 더 바람직하다고 할 수 있다.

### O(1)

- 입력값에 상관 없이 언제나 일정한 시간이 걸리는 알고리즘

### O(n)

- 입력데이터의 크기에 비례해서 처리 시간이 걸리는 알고리즘
- 길이

```jsx
const function = () => {
  for (let i = 0; i < n; i += 1) {
    console.log(i);
  }
};
```

- 데이터랑 시간이 같은 비율로 증가함

### O(n^2)

- n개의 루프를 n번 돌리는 알고리즘
- 면적

```jsx
const function = () => {
  for (let j = 0; j < n; j += 1) {
    for (let i = 0; i < n; i += 1) {
      console.log(i + j);
    }
  }
};
```

### O(nm)

- n개의 루프를 m번 돌리는 알고리즘

```jsx
const function = () => {
  for (let j = 0; j < m; j += 1) {
    for (let i = 0; i < n; i += 1) {
      console.log(i + j);
    }
  }
};
```

### O(n^3)

- n^2을 n 번 돌리는 알고리즘
- 부피

```jsx
const function = () => {
  for (let k = 0; k < n; k += 1) {
    for (let j = 0; j < n; j += 1) {
      for (let i = 0; i < n; i += 1) {
        console.log(i + j);
      }
    }
  }
};
```

### O(2^n) or O(m^n)

- 피보나치

```jsx
const fibo = (n, r) => {
  if (n <= 0) return 0;
  else if (n === 1) return (r[n] = 1);
  else r[n] = fibo(n - 1, r) + fibo(n - 2, r);
};
```

### O(log n)

- 한 번 연산할 때마다, 검색해야 하는 데이터의 양이 절반씩 떨어지는 알고리즘
- 이진탐색트리
- 데이터가 증가해도 성능이 그렇게 차이나지 않는다

```jsx
const function = (num,arr,start,end) => {
	if(start > end) return -1;
	middle = ( start + end) / 2;
	if(arr[middle] === num) return middle
	else if(arr[middle] > num) return function(num,arr,start,middle-1)
	else return function(num,arr,middle+1,end)

}
```

### O(nlog n)

- nlogn이라는 수 자체에 대해서 아직 개념이 잡히지 않았던 것 같다. logn이 n번 연산되는것이니, logn의 시간 복잡도를 가지는 이진탐색트리를 n번 연산하면 되지 않나? 하는 이상한 질문도 했었다.
- 퀵소트, 힙소트, 머지소트의 경우 nlogn의 시간 복잡도를 가지게 된다(참고 [블로그](https://codingdog.tistory.com/entry/%ED%80%B5-%EC%A0%95%EB%A0%AC-%ED%8F%89%EA%B7%A0-%EC%8B%9C%EA%B0%84-%EB%B3%B5%EC%9E%A1%EB%8F%84-%EC%99%9C-Onlogn%EC%9D%BC%EA%B9%8C) )
- 이진탐색트리의 경우에는 기준을 잡고 기준보다 크거나 작으면 반대편은 아예 탐색하지 않으므로 logn의 시간복잡도를 가지게 되고, 퀵소트 등의 경우에는 pivot을 잡고, 반대편은 버리는 것이 아니라 반대편까지도 탐색을 해야 하기 때문에 logn을 n번 하게 되는 연산을 거치게 된다.
