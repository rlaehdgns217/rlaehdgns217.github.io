---
layout: post
date: 2021-01-03 23:40:00
title: "react-native 초기 세팅 및 프로그래머스 문제 풀이 "
author: 김동훈
categories: [TIL]
tags: [github]
image: https://braze-marketing-assets.s3.amazonaws.com/images/partner_logos/react-native.png
rating: 2
---

# RN 초기 세팅

사이드 프로젝트를 sr단계까지는 했는데, 연말이다 뭐다 겹치면서 아직 시작을 하지는 못했다. 그렇기 때문에 이번 신년 연휴가 지나면 작업에 들어가려고, 연휴동안 코드를 찍을 수 있는 준비를 하는 것이 필요했다. 죄송스럽게도 함께 하는 팀원분이 엄청난 삽질을 통해 알아낸 것을 옆에서 주워먹었고, 이렇게 적게 되었다.
팀원 분과 상황이 달라서 나는 오류 없이 진행이 되었다.

### 초기 세팅

- brew install node (node는 이미 로컬에 설치가 되어 있었기 때문에, 따로 설치를 하지는 않았다.)
- brew install watchman (watchman이 뭐하는지 모르지만, 공식문서에서 그냥 조용하고 깔라고 해서 설치했다. 나중에 찾아보니 file watching service라고 한다.)
- brew install --cask adoptopenjdk/openjdk/adoptopenjdk8 (이것 또한 뭔지도 모르고 일단 설치했다.)

### 안드로이드 sdk 설정

- 안드로이드 스튜디오 실행
- 하단부 configure 선택
- sdk 플랫폼 > show package detail 선택(하면 안드로이드 버전별로 여러가지 선택할 수 있는 체크박스가 나온다.)
- 나의 경우에는 android 9.0을 선택했고,

```
Android SDK Platform 28
Intel x86 Atom System Image
Google APIs Intel x86 Atom System Image
Google APIs Intel x86 Atom_64 System Image
```

- 위와 같은 것을 선택해서 설치했다.

### 스튜디오 환경 변수 설정

- 로컬에서 vi ./bash_profile을 입력해서 vim을 통해 수정을 했고,

```
export ANDROID_HOME=자신의 안드로이드SDK 위치/Android/sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools
```

- 위와 같이 입력했다.
- 중간 자신의 경로는 안드로이드스튜디오의 sdk 설정화면에 가면 상단부에서 알 수 있다. 그대로 복붙해서 사용

- source ~/.bash_profile
- adb
  위의 명령어를 입력하게 되서 잘 진행이 되었다면 version을 확인 할 수 있는 텍스트들이 터미널에 노출된다.
- npx react-native run-android를 입력하고, 이것저것 설치가 진행된 후 리액트 초기화면이 나오게 된다.

참고 블로그 : https://codefabian.github.io/TIL/devlog/11.2021.01.03

### after

- 솔직히 초기 세팅을 혼자서 하라고 하면 아직 자신이 없다. 굳이 React-native가 아니더라도.. 이제까지 사용했던 스택들을 다시 처음부터 세팅하라고 하면 여러가지로 당황스러울 것 같다.
- 하지만.. 팀원분의 삽질을 옆에서 보면서, 삽질을 통해 배우는게 무엇인지 다시 느낄 수 있었고, 혼자서 했을 때보다는 효율적으로 진행이 되지 않았나 하고 생각은 해본다..ㅋㅋ
- 공식문서도 꼼꼼히 읽어봐야 하고..
- 뭔지도 모르고 설치했던 부분을 파고 들어갈 필요성도 느끼게 됐다.

---

# 크레인 인형뽑기 게임

### **문제 설명**

게임개발자인 죠르디는 크레인 인형뽑기 기계를 모바일 게임으로 만들려고 합니다.죠르디는 게임의 재미를 높이기 위해 화면 구성과 규칙을 다음과 같이 게임 로직에 반영하려고 합니다.

![https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/69f1cd36-09f4-4435-8363-b71a650f7448/crane_game_101.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/69f1cd36-09f4-4435-8363-b71a650f7448/crane_game_101.png)

게임 화면은 **1 x 1** 크기의 칸들로 이루어진 **N x N** 크기의 정사각 격자이며 위쪽에는 크레인이 있고 오른쪽에는 바구니가 있습니다. (위 그림은 5 x 5 크기의 예시입니다). 각 격자 칸에는 다양한 인형이 들어 있으며 인형이 없는 칸은 빈칸입니다. 모든 인형은 1 x 1 크기의 격자 한 칸을 차지하며 **격자의 가장 아래 칸부터 차곡차곡 쌓여 있습니다.** 게임 사용자는 크레인을 좌우로 움직여서 멈춘 위치에서 가장 위에 있는 인형을 집어 올릴 수 있습니다. 집어 올린 인형은 바구니에 쌓이게 되는 데, 이때 바구니의 가장 아래 칸부터 인형이 순서대로 쌓이게 됩니다. 다음 그림은 [1번, 5번, 3번] 위치에서 순서대로 인형을 집어 올려 바구니에 담은 모습입니다.

![https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/638e2162-b1e4-4bbb-b0d7-62d31e97d75c/crane_game_102.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/638e2162-b1e4-4bbb-b0d7-62d31e97d75c/crane_game_102.png)

만약 같은 모양의 인형 두 개가 바구니에 연속해서 쌓이게 되면 두 인형은 터뜨려지면서 바구니에서 사라지게 됩니다. 위 상태에서 이어서 [5번] 위치에서 인형을 집어 바구니에 쌓으면 같은 모양 인형 **두 개**가 없어집니다.

![https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/8569d736-091e-4771-b2d3-7a6e95a20c22/crane_game_103.gif](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/8569d736-091e-4771-b2d3-7a6e95a20c22/crane_game_103.gif)

크레인 작동 시 인형이 집어지지 않는 경우는 없으나 만약 인형이 없는 곳에서 크레인을 작동시키는 경우에는 아무런 일도 일어나지 않습니다. 또한 바구니는 모든 인형이 들어갈 수 있을 만큼 충분히 크다고 가정합니다. (그림에서는 화면표시 제약으로 5칸만으로 표현하였음)

게임 화면의 격자의 상태가 담긴 2차원 배열 board와 인형을 집기 위해 크레인을 작동시킨 위치가 담긴 배열 moves가 매개변수로 주어질 때, 크레인을 모두 작동시킨 후 터트려져 사라진 인형의 개수를 return 하도록 solution 함수를 완성해주세요.

### **[제한사항]**

- board 배열은 2차원 배열로 크기는  이상  이하입니다.

  5 x 5

  30 x 30

- board의 각 칸에는 0 이상 100 이하인 정수가 담겨있습니다.
  - 0은 빈 칸을 나타냅니다.
  - 1 ~ 100의 각 숫자는 각기 다른 인형의 모양을 의미하며 같은 숫자는 같은 모양의 인형을 나타냅니다.
- moves 배열의 크기는 1 이상 1,000 이하입니다.
- moves 배열 각 원소들의 값은 1 이상이며 board 배열의 가로 크기 이하인 자연수입니다.

### **입출력 예**

[제목 없음](https://www.notion.so/e98c6b2b160c40e0838fadf2802b449c)

### **입출력 예에 대한 설명**

**입출력 예 #1**

인형의 처음 상태는 문제에 주어진 예시와 같습니다. 크레인이 [1, 5, 3, 5, 1, 2, 1, 4] 번 위치에서 차례대로 인형을 집어서 바구니에 옮겨 담은 후, 상태는 아래 그림과 같으며 바구니에 담는 과정에서 터트려져 사라진 인형은 4개 입니다.

### 코드

```jsx
function solution(board, moves) {
  var answer = 0;
  var arr = [];
  var num = moves.map((n) => {
    return n - 1;
  });

  for (let n = 0; n < num.length; n += 1) {
    for (let i = 0; i < board.length; i += 1) {
      if (board[i][num[n]] !== 0) {
        arr.push(board[i][num[n]]);
        board[i][num[n]] = 0;
        break;
      }
    }
  }

  const removeDoll = (arr) => {
    for (let i = 1; i < arr.length; i += 1) {
      if (arr[i - 1] === arr[i]) {
        arr.splice(i - 1, 2);
        answer = answer + 2;
        removeDoll(arr);
      }
    }
  };

  removeDoll(arr);

  return answer;
}
```

- 뽑은 인형까지는 board를 하나씩 보면서 구했다.
- 우선 2중 배열이므로 i가 board의 y축의 진행방향이 된다. [0],[1],[2],[3],[4]...

  ```jsx
  // [0, 0, 0, 0, 0] -----------i =0
  // [0, 0, 1, 0, 3] -----------i =1
  // [0, 2, 5, 0, 1] -----------i =2
  // [4, 2, 4, 4, 2] -----------i =3
  // [3, 5, 1, 3, 1] -----------i =4
  //  1- 2- 3- 4- 5  -----------n
  ```

- moves의 요소들(n)은 x축의 진행방향이 된다.
- 또한 moves의 요소들은 크기가 한정되어 있다.(위의 예시의 경우, 5가 최대 값)
- 위의 경우에서 moves의 0번째 요소값은 1이고 i가 0~2일때의 값이 0(인형이 없음)이기 때문에, i는 3일때의 n=1, i=3일때의 값이 바구니(arr)에 담겨야 한다.
- 인덱스랑 맞추기 위해 map을 사용 해서 moves에서 -1씩. >> index는 0부터 시작하지만 moves는 1이 기준이기 때문에
- 그렇게 해서 moves의 length 만큼 for문을 실행하게 되고, (1회 순회 할 때마다 i는 0부터 4까지 순회)
- 바구니(arr)에 넣어진 인형은 없어진다(0을 할당)
- 인형을 빼도(arr.push) i가 순회되면서 밑에 있는 인형을 한 번 더 넣기 때문에, 조건에 맞는 것을 바구니에 넣는다면 break로 순회를 멈춰주었다.
- 그렇게 해서 moves 배열이 다 돌게 되면 바구니에는 moves의 length만큼 인형이 쌓이는데, 입출력 예시의 경우 1번라인에서 세번의 뽑기가 진행 되기 때문에, 인형이 없는 것으로 처리되어 한 번은 아무 일도 일어나지 않는다.

```jsx
arr = [4, 3, 1, 1, 3, 2, 4];
```

- 위와 같은 배열을 가질 때, 인접해 있는 숫자가 있다면, splice를 사용해 이 숫자들을 지워주고, 똑같은인형이 있어야만 지워지는것이기 때문에, 1번 지울때마다 answer에 2를 더해준다.
- 이와 같은 과정을 재귀함수로 만들어, 인접한 수가 똑같지 않을 때까지 재귀를 사용한다.
- 결과값은 똑같은 수가 인접했을 때의 경우의 수 \* 2(인형을 둘 다 지워주기 때문에)

---

## 모의고사

### **문제 설명**

수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.

1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.

### 제한 조건

- 시험은 최대 10,000 문제로 구성되어있습니다.
- 문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
- 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.

### 입출력 예

| answers     | return  |
| ----------- | ------- |
| [1,2,3,4,5] | [1]     |
| [1,3,2,4,2] | [1,2,3] |

### 입출력 예 설명

입출력 예 #1

- 수포자 1은 모든 문제를 맞혔습니다.
- 수포자 2는 모든 문제를 틀렸습니다.
- 수포자 3은 모든 문제를 틀렸습니다.

따라서 가장 문제를 많이 맞힌 사람은 수포자 1입니다.

입출력 예 #2

- 모든 사람이 2문제씩을 맞췄습니다.
- **[solution.js](https://programmers.co.kr/learn/courses/30/lessons/42840#)**

1

```
function solution(answers) {
```

2

```
    var answer = [];
```

### 코드

```jsx
function solution(answers) {
  var answer = [];
  var result = [];
  var answer1 = [1, 2, 3, 4, 5];
  var answer2 = [2, 1, 2, 3, 2, 4, 2, 5];
  var answer3 = [3, 3, 1, 1, 2, 2, 4, 4, 5, 5];
  var grades = [0, 0, 0];

  for (let i = 0; i < answers.length; i += 1) {
    if (answer1[i % 5] === answers[i]) {
      grades[0] = grades[0] += 1;
    }
    if (answer2[i % 8] === answers[i]) {
      grades[1] = grades[1] += 1;
    }
    if (answer3[i % 10] === answers[i]) {
      grades[2] = grades[2] += 1;
    }
  }

  for (let j = 0; j < grades.length; j += 1) {
    if (grades[j] === Math.max(...grades)) {
      answer.push(j + 1);
    }
  }

  return answer;
}
```

- i % array.length를 하게 되면, 배열끼리의 수를 맞출 수 있는 부분을 배웠다. 코드에서

  ```jsx
  for(let i = 0; i < answers.length; i += 1)
  ```

  이 부분은 answers의 배열만 순회를 하는데, 이렇게 하면 answer1의 배열의 길이가 answers와 다르다면 index가 부족해, undefinded가 뜨는 경우가 생긴다. 그렇다고 for문안에 다시 for문을 넣는다면 시간복잡도가 너무 올라가고, 효율적이지 못한 코드가 된다. i를 단순히 index로만 생각하는것이 아니라, i를 다루는 것도 많이 연습해봐야 할 부분 같다.

- 처음에는 if, else if로 조건을 분기했다. 문제가 없다고 생각했지만, 두번째 테스트케이스 ([1,3,2,4,2])에서 return은 3가지가 나와야 하지만 두가지만 나오는 경우가 생겼다. 원인을 찾아보니, answer3과 answer2가 같이 겹치는 경우가 있었다.

---

# 두 개 뽑아서 더하기

### 입출력 예

| numbers     | result        |
| ----------- | ------------- |
| [2,1,3,4,1] | [2,3,4,5,6,7] |
| [5,0,2,7]   | [2,5,7,9,12]  |

### 입출력 예 설명

입출력 예 #1

- 2 = 1 + 1 입니다. (1이 numbers에 두 개 있습니다.)
- 3 = 2 + 1 입니다.
- 4 = 1 + 3 입니다.
- 5 = 1 + 4 = 2 + 3 입니다.
- 6 = 2 + 4 입니다.
- 7 = 3 + 4 입니다.
- 따라서 `[2,3,4,5,6,7]` 을 return 해야 합니다.

입출력 예 #2

- 2 = 0 + 2 입니다.
- 5 = 5 + 0 입니다.
- 7 = 0 + 7 = 5 + 2 입니다.
- 9 = 2 + 7 입니다.
- 12 = 5 + 7 입니다.
- 따라서 `[2,5,7,9,12]` 를 return 해야 합니다.

### 코드

```jsx
function solution(numbers) {
  var answer = [];
  for (let i = 0; i < numbers.length; i += 1) {
    for (let j = 0; j < numbers.length; j += 1) {
      if (i !== j) {
        if (!answer.includes(numbers[i] + numbers[j])) {
          answer.push(numbers[i] + numbers[j]);
        }
      }
    }
  }
  return answer.sort((a, b) => a - b);
}
```
