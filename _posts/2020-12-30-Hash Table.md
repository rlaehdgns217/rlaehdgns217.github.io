---
layout: post
date: 2020-12-30 23:00:00
title: "Hash Table "
author: 김동훈
categories: [TIL]
tags: [github]
image: https://5.imimg.com/data5/TK/YX/MK/SELLER-1943297/data-structures-training-in-gurgaon-500x500.png
rating: 2
---

# Data structure

---

해시테이블은 key와 value로 데이터를 저장하는 데이터 스트럭쳐입니다.
value값이 배열의 형태로 저장되기 때문에, 빠르게 데이터를 검색 할 수 있습니다.
해시 테이블은 각각의 Key값에 해시함수를 적용해 배열의 고유한 index를 생성하고, 이 index를 활용해 값을 저장하거나 검색하게 됩니다.
여기서 실제 값이 저장되는 장소를 버킷 또는 슬롯이라고 합니다.
키를 가진 테이블이 있고, 키마다 버킷을 할당해서 버킷에 데이터를 저장하게 됩니다.
해시테이블을 사용하는 예시는 전화번호부를 예시로 들 수 있을 것 같습니다.
김코딩, 박해커라는 사람들과 홍길동이라는 이름을 가진 사람 2명 총 4명이 있다고 가정할 때, 각 사람별로 키값에 할당되고, 홍길동이라는 키의 버킷에는 두개의 다른 전화번호가 들어갈 것입니다.

(수정 할 것)
