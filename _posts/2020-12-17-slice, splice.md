---
layout: post
date: 2020-12-17 24:00:00
title: 'slice vs splice'
author: 김동훈
categories: [TIL]
tags: [github]
image: https://joshua1988.github.io/images/posts/web/javascript/js.png
rating: 3
---

# slice, splice의 차이점

생성일: 2020년 12월 17일 오후 11:01


- slice(start[, end])

  - 기존의 배열을 변경하지 않는 새로운 배열을 리턴한다.

  ```jsx
  var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
  var arr1 = arr.slice(3, 5); // [4, 5]
  
  //이때 메모리에는 arr과 arr1 두개의 배열이 들어가 있다.
  ```

- splice(start[, deleteCount[, item1[, item2[, ...]]]])

  - 기존의 배열을 변경해서 리턴한다.

  ```jsx
  var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12];
  var arr1 = arr.splice(10, 2, 'a', 'b', 'c');
  console.log(arr); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, "a", "b", "c"]
  console.log(arr1); // [11, 12]
  //메모리에는 arr 하나만 있고, 기존의 arr이 아닌 새롭게 변경 된 arr이 리턴된다.
  ```

두 메소드의 차이는 얕은 복사와 깊은 복사의 차이로 볼 수 있다. 

얕은 복사가 복합객체(리스트)만 복사되고 그 안의 내용은 동일한 객체를 참조한다면, 깊은 복사의 경우에는 복합객체를 새롭게 생성하고 그 안의 내용까지 재귀적으로 새롭게 생성하게 된다.(slice > 깊은 복사, splice > 얕은복사) 각 메소드별로 가리키는 참조값이 다르기 때문에, 상황에 맞게 쓸 수 있어야 한다.